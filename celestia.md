# Celestia Light Node setup

### Update packages
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

### Install utils
```bash
sudo apt install curl build-essential git wget jq make gcc tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev lz4 -y
```

### Install Go
```bash
ver="1.23.2" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```

###  Set ufw alowance
```bash
sudo ufw allow 2121 comment light_node
```

### Install binaries
```bash
cd $HOME
rm -rf celestia-node
git clone https://github.com/celestiaorg/celestia-node.git
cd celestia-node/
git checkout tags/v0.18.3-mocha
make build
sudo make install
```

### Build cel-key
```bash
 make cel-key
mv $HOME/celestia-node/cel-key /usr/local/bin/
```

### Create wallet
```bash
   celestia light init --p2p.network mocha
```

### Show wallet
```bash
   celestia light start --core.ip rpc-mocha.pops.one --p2p.network mocha
   
### Initialize Light node

```bash
celestia light init \
  --core.ip 8.52.247.236 \
  --p2p.network mocha \
  --core.rpc.port 26657 \
  --core.grpc.port 9090 \
  --keyring.keyname light_wallet
```

### Сreate service file
```bash
sudo tee <<EOF >/dev/null /etc/systemd/system/celestia-light.service
[Unit]
Description=celestia-light testnet daemon
After=network-online.target

[Service]
User=$USER
ExecStart=$(which celestia) light start \
  --p2p.network mocha \
  --metrics.tls=true --metrics --metrics.endpoint otel.celestia-mocha.com \
  --keyring.keyname light_wallet
  
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
### Start service and check logs

```bash
sudo systemctl daemon-reload
sudo systemctl enable celestia-light
sudo systemctl restart celestia-light && sudo journalctl -u celestia-light -f -o cat
```

### Check node id
```bash
celestia p2p info --node.store ~/.celestia-light-mocha-4/
```
