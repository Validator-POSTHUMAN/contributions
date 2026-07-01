# Monad FastLane Sidecar Guide for Validators

Last updated: 2026-07-01

This guide helps Monad validators prepare, install, verify, monitor, and
upgrade the FastLane / shMonad MEV sidecar safely.

It is validator-neutral. Replace every placeholder with your own operator
inventory and the values received during shMonad onboarding.

## Scope

The FastLane sidecar is an operational integration for Monad validators. It is
not only a listing request. A typical integration touches:

- shMonad onboarding and validator-specific coinbase contract;
- Monad beneficiary / coinbase routing;
- FastLane dedicated fullnode identities;
- monad-bft and monad-rpc mempool IPC socket paths;
- rootless Docker under a dedicated fastlane user;
- release signature, image signature, and provenance verification;
- sidecar health, metrics, logs, and alerting.

## Official Sources

- shMonad validator onboarding:
  https://docs.shmonad.xyz/validators/onboarding
- Validator setup:
  https://docs.shmonad.xyz/validators/onboarding/validator-setup
- Rootless Docker sidecar install:
  https://docs.shmonad.xyz/validators/onboarding/install-sidecar-rootless-docker
- Stake allocation:
  https://docs.shmonad.xyz/stake-allocation
- FastLane sidecar repository:
  https://github.com/FastLane-Labs/fastlane-sidecar
- POSTHUMAN FastLane sidecar AI skill:
  https://github.com/Validator-POSTHUMAN/AI-skills-for-networks/blob/main/fastlane-sidecar/SKILL.md

Always re-read the official docs before a production install or upgrade.

## Preconditions

Before installing:

- Monad validator is running and synced.
- monad-bft version is v0.12.6 or newer. FastLane docs state older versions
  can connect while tx_received stays at 0.
- shMonad onboarding is complete enough for your validator:
  - validator-specific coinbase contract received;
  - beneficiary update approved by the operator;
  - FastLane fullnode pubkeys received;
  - sidecar version selected.
- You know your actual service names and paths.
- You have a rollback plan and config backups.

## Order of Operations

Official shMonad onboarding order matters:

1. Complete shMonad onboarding.
2. Receive validator-specific coinbase contract.
3. Update Monad beneficiary to the coinbase contract.
4. Add FastLane dedicated fullnodes.
5. Install and run the sidecar.
6. Verify revenue path, sidecar health, and monitoring.

Do not skip directly to the sidecar if the coinbase / beneficiary path is not
clear.

## Preflight Snapshot

Capture current state before changing anything:

~~~bash
systemctl is-active monad-bft monad-execution monad-rpc || true
systemctl cat monad-bft
systemctl cat monad-rpc
ps -eo pid,user,args | grep -E 'monad-node|monad-rpc|fastlane-sidecar' | grep -v grep || true

curl -fsS http://127.0.0.1:8080/ \
  -H 'Content-Type: application/json' \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}'

curl -fsS http://127.0.0.1:8080/ \
  -H 'Content-Type: application/json' \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_syncing","params":[]}'
~~~

Back up service state and config:

~~~bash
TS=$(date -u +%Y%m%dT%H%M%SZ)
mkdir -p "$HOME/backups/monad-fastlane-sidecar-$TS"

systemctl cat monad-bft > "$HOME/backups/monad-fastlane-sidecar-$TS/monad-bft.systemctl-cat.txt"
systemctl cat monad-rpc > "$HOME/backups/monad-fastlane-sidecar-$TS/monad-rpc.systemctl-cat.txt"
cp -a /home/monad/monad-bft/config/node.toml "$HOME/backups/monad-fastlane-sidecar-$TS/node.toml"
~~~

Do not publish backups if they contain operator-specific values.

## Beneficiary and FastLane Fullnodes

The beneficiary / coinbase contract and FastLane fullnode pubkeys are received
during onboarding. Treat them as operator-specific configuration.

If the task includes a beneficiary change:

1. Back up node.toml.
2. Set the beneficiary to the validator-specific coinbase contract.
3. Restart only the service required by current official docs.
4. Verify local RPC, service health, and logs.

For FastLane fullnodes, official docs use node.toml fullnode_dedicated
identities. If an empty inline assignment already exists, remove or comment it
before adding array-of-table entries.

FastLane docs describe live reload with monad-debug-node when supported:

~~~bash
monad-debug-node \
  --control-panel-ipc-path /home/monad/monad-bft/controlpanel.sock \
  reload-config
~~~

Verify reload result in monad-bft logs.

## Segregated Mempool IPC Socket

The sidecar only needs access to the Monad mempool socket. The safer pattern is
to move that socket into a dedicated directory accessible to fastlane, not to
grant access to unrelated validator files.

Create the IPC directory and ACLs:

~~~bash
sudo useradd -m -s /bin/bash fastlane || true
echo "SIDECAR_NETWORK=mainnet" | sudo tee /home/fastlane/.env
sudo chown fastlane:fastlane /home/fastlane/.env

sudo install -d -o monad -g monad -m 2750 /var/run/monad-ipc
sudo setfacl -m u:fastlane:rx /var/run/monad-ipc
sudo setfacl -d -m u:fastlane:rw /var/run/monad-ipc
sudo loginctl enable-linger fastlane
~~~

Use testnet instead of mainnet in SIDECAR_NETWORK when appropriate.

## Systemd Drop-ins

Use systemctl edit. Do not edit installed unit files directly.

Important: in a Service drop-in, ExecStart= replaces the whole command. Copy
the full original ExecStart from systemctl cat and change only the intended
IPC flag.

For monad-bft:

- preserve every original flag;
- change --mempool-ipc-path to /var/run/monad-ipc/mempool.sock;
- recreate IPC directory and ACLs at service start because /var/run is tmpfs;
- use UMask=0007 so socket ACL write access is not masked away.

For monad-rpc:

- preserve every original flag;
- change --ipc-path to /var/run/monad-ipc/mempool.sock.

After editing:

~~~bash
sudo systemctl daemon-reload
sudo systemctl restart monad-bft monad-execution monad-rpc
sudo systemctl status monad-bft monad-execution monad-rpc --no-pager -l
~~~

Verify process flags and socket permissions:

~~~bash
ps -eo pid,user,args | grep -E 'monad-node|monad-rpc' | grep -v grep
ls -l /var/run/monad-ipc /var/run/monad-ipc/mempool.sock
getfacl -p /var/run/monad-ipc /var/run/monad-ipc/mempool.sock
~~~

## Rootless Docker and Sidecar

Install rootless Docker dependencies according to current official docs.

The compose file should:

- run as fastlane, not root;
- pin image by digest, not only tag;
- run read-only;
- drop all Linux capabilities;
- enable no-new-privileges;
- set memory / pids / CPU limits;
- mount only /var/run/monad-ipc;
- expose metrics on 127.0.0.1:8765 by default.

Example compose shape:

~~~yaml
services:
  fastlane-sidecar:
    image: ghcr.io/fastlane-labs/fastlane-sidecar:<SIDECAR_VERSION>@<SIDECAR_DIGEST>
    container_name: fastlane-sidecar
    restart: unless-stopped
    read_only: true
    cap_drop: [ALL]
    security_opt:
      - no-new-privileges:true
    pids_limit: 256
    mem_limit: 512m
    memswap_limit: 512m
    cpuset: "12-15"
    volumes:
      - /var/run/monad-ipc:/var/run/monad-ipc
    ports:
      - "127.0.0.1:8765:8765"
    command:
      - --log-level=info
      - --network=<SIDECAR_NETWORK>
      - --monitoring-port=8765
      - --txpool-socket=/var/run/monad-ipc/mempool.sock
~~~

Adjust cpuset for your host.

## Release Verification

Before running a sidecar version:

1. Import the FastLane release public key from the official source.
2. Download the release manifest and signature.
3. Verify the GPG signature.
4. Extract the digest from the signed manifest.
5. Verify the image with cosign.
6. Verify SLSA provenance with gh attestation verify or cosign attestation.
7. Write SIDECAR_VERSION and SIDECAR_DIGEST into /home/fastlane/.env.

Do not run an unverified floating tag in production.

## Start and Verify

Run as fastlane:

~~~bash
docker compose -f /home/fastlane/compose.yml pull
docker compose -f /home/fastlane/compose.yml up -d
docker ps --filter name=fastlane-sidecar
docker inspect fastlane-sidecar --format '{{.Image}}'
~~~

Health:

~~~bash
curl -fsS http://127.0.0.1:8765/health | jq
curl -fsS http://127.0.0.1:8765/metrics | head
docker logs --tail 100 fastlane-sidecar
~~~

Expected:

- last_received_at is recent once the sidecar is receiving data.
- tx_received becomes nonzero after enough time / leader proximity.
- Metrics endpoint is loopback-reachable.
- Logs do not show repeated socket connection failures.

tx_received can remain 0 briefly. If it stays 0, check BFT version, socket
path, ACLs, monad-bft flags, monad-rpc flags, and sidecar logs.

## Monitoring

Minimum alert coverage:

- monad-bft, monad-execution, monad-rpc active;
- fastlane-sidecar container running;
- /health reachable;
- last_received_at freshness;
- tx_received behavior over a reasonable window;
- /metrics reachable from the monitoring host;
- socket path and ACL sanity;
- restart count / repeated sidecar error logs.

Keep webhook, Telegram, Slack, Prometheus, and OTel credentials outside public
repos.

## Upgrade

1. Record current image digest and health output.
2. Download and verify the new signed release manifest.
3. Verify image signature and provenance.
4. Update only SIDECAR_VERSION and SIDECAR_DIGEST in /home/fastlane/.env.
5. Pull and restart compose.
6. Verify digest, /health, /metrics, and logs.

Rollback is the previous digest plus docker compose pull/up.

## Rollback

Container-only rollback:

~~~bash
# as fastlane
docker compose -f /home/fastlane/compose.yml down
# restore previous SIDECAR_VERSION and SIDECAR_DIGEST in /home/fastlane/.env
docker compose -f /home/fastlane/compose.yml pull
docker compose -f /home/fastlane/compose.yml up -d
~~~

Full wiring rollback:

1. Restore backed-up monad-bft and monad-rpc drop-ins/config.
2. Run systemctl daemon-reload.
3. Restart affected Monad services.
4. Verify local RPC health and logs.

Beneficiary rollback affects revenue routing. Do it only with explicit
operator confirmation.
