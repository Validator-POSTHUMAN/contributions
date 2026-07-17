# POSTHUMAN Supports Arc

POSTHUMAN supports Arc Network through independent infrastructure operation,
testing, and public technical documentation. Arc is the infrastructure;
POSTHUMAN remains the primary identity for these services and materials.

## Contributions to date

### Non-signing testnet full node

POSTHUMAN built an Arc testnet full node from source in April 2026 and
configured both execution and consensus layers, official snapshots, follow
mode relay endpoints, local metrics, and service supervision.

Operational testing identified the mandatory Zero5/Zero6 upgrade boundary.
The node was upgraded from `v0.6.0` to `v0.7.2` on 17 July 2026 and verified
past the previously rejected fork block. This is a non-signing full node, not
a validator and not a public RPC endpoint.

### Public node installation guide

POSTHUMAN publishes a security-focused Arc testnet node guide with:

- release checksum verification;
- official snapshot bootstrap;
- loopback-bound RPC and metrics;
- local IPC between execution and consensus layers;
- independent height comparison;
- upgrade rollback preparation and troubleshooting notes.

The guide is available in the **Install Guide** tab on this page.

### Operational research

Our testing covers Arc's execution/consensus architecture, follow-mode relay
behavior, snapshot recovery requirements, hard-fork compatibility, monitoring
signals, and the difference between process state and actual chain progress.

## Future contribution direction

POSTHUMAN plans to build on this operational experience through:

- reproducible monitoring and troubleshooting guidance;
- an AI-agent skill for safe Arc node operations;
- issue reports or pull requests to the Arc repositories when backed by a
  reproducible upstream problem or a tested generic improvement;
- direct technical feedback and coordination with the Arc community.

No upstream Arc pull request is claimed on this page. No formal partnership or
endorsement is implied.

## Official Arc resources

- Website: https://www.arc.io/
- Documentation: https://docs.arc.network/
- Node repository: https://github.com/circlefin/arc-node
- Community: https://community.arc.io/
- Partner guidelines: https://www.arc.io/brand-guidelines-and-partner-toolkit

Arc is a trademark of Circle Internet Group, Inc. and/or its affiliates.
