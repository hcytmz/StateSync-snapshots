<h1 align="center"> 🔥SGE Mainnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/SGE)
=

<h1 align="center"> MAINNET</h1>

# StateSync Sge Mainnet
```python
SNAP_RPC=https://sge.rpc.m.stavr.tech:443
peers="58a458a7136da7e8cc55357999aa89f5fd262588@sge.peers.stavr.tech:1156"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$peers'"|' $HOME/.sge/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.sge/config/config.toml
sged tendermint unsafe-reset-all --home /root/.sge
wget -O $HOME/.sge/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/addrbook.json"
systemctl restart sged && journalctl -u sged -f -o cat
```
# SnapShot Sge Mainnet (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sged
cp $HOME/.sge/data/priv_validator_state.json $HOME/.sge/priv_validator_state.json.backup
rm -rf $HOME/.sge/data
curl -o - -L http://sge.snapshot.stavr.tech:1003/sge/sge-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.sge --strip-components 2
mv $HOME/.sge/priv_validator_state.json.backup $HOME/.sge/data/priv_validator_state.json
wget -O $HOME/.sge/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/addrbook.json"
sudo systemctl restart sged && journalctl -u sged -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/SGE/Testnet)
=

# StateSync Sge Testnet
```python
SNAP_RPC=https://sge.rpc.t.stavr.tech:443
peers="e2c5f2a902b7e6b8c006008e962ab4ddd70cdd78@sge.peers-t.stavr.tech:1146"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$peers'"|' $HOME/.sge/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.sge/config/config.toml
sged tendermint unsafe-reset-all --home /root/.sge
wget -O $HOME/.sge/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/Testnet/addrbook.json"
systemctl restart sged && journalctl -u sged -f -o cat
```

# SnapShot Sge Testnet (~0.2GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sged
cp $HOME/.sge/data/priv_validator_state.json $HOME/.sge/priv_validator_state.json.backup
rm -rf $HOME/.sge/data
curl -o - -L http://sge-t.snapshot.stavr.tech:1017/sget/sget-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.sge --strip-components 2
mv $HOME/.sge/priv_validator_state.json.backup $HOME/.sge/data/priv_validator_state.json
wget -O $HOME/.sge/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/SGE/addrbook.json"
sudo systemctl restart sged && journalctl -u sged -f -o cat

```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Sge-Mainnet       `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Sge-Testnet       `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://sge.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://sge.api.t.stavr.tech \
🔥RPC Mainnet🔥:           https://sge.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥RPC Testnet🔥:           https://sge.rpc.t.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC Mainnet🔥:          http://sge.grpc.m.stavr.tech:543 \
🔥gRPC Testnet🔥:          http://sge.grpc.t.stavr.tech:242 \
🔥peer Mainnet🔥:					 `58a458a7136da7e8cc55357999aa89f5fd262588@sge.peers.stavr.tech:1156` \
🔥peer Testnet🔥:					 `e2c5f2a902b7e6b8c006008e962ab4ddd70cdd78@sge.peers-t.stavr.tech:1146` \
🔥Genesis Mainnet🔥:				```wget -O $HOME/.sge/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/genesis.json"``` \
🔥Genesis Testnet🔥:				```wget -O $HOME/.sge/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/Testnet/genesis.json"``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.sge/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.sge/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/Testnet/genesis.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O sggem https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/sggem && chmod +x sggem && ./sggem``` \
🔥Auto_install script Testnet🔥: ```wget -O sgge https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/SGE/Testnet/sgge && chmod +x sgge && ./sgge``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Sge/Decentralization)🔥

<details>
<summary>RPC Scanning</summary>

<h2 align="center"> We scan nodes in real time every 4 hours. And we provide the final result of RPC endpoints.
We cannot influence the operation of these nodes in any way. </h2>


```python
If Voting Power is higher than 0 --> then the Node is a validator of the network and may be subject to attack and be a potential threat to the chain.
```
```python
We marked such validators with a red symbol
```

</details>

[raw json Mainnet](https://rpc-check.sgem.stavr.tech/sgem/rpc-sgem-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Sge/Rpc-Check-Testnet)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>142.132.202.86:16657</td><td>sgenet-1</td><td>ramuchi.tech 🟢</td><td>2749273</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T03:20:44.743988511UTC</td></tr><tr><td>3.37.63.177:26657</td><td>sgenet-1</td><td>sge-sentry-1 🟢</td><td>2749277</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T03:21:13.501661498UTC</td></tr><tr><td>94.130.36.146:16702</td><td>sgenet-1</td><td>ruangnode 🔴</td><td>2749276</td><td>1226627</td><td>False</td><td>on</td><td>4000028</td><td>2024-03-12T03:21:11.804825184UTC</td></tr><tr><td>65.109.88.254:32657</td><td>sgenet-1</td><td>ksalab 🔴</td><td>2749271</td><td>1496501</td><td>False</td><td>on</td><td>3999602</td><td>2024-03-12T03:20:38.152357692UTC</td></tr><tr><td>158.69.27.233:20657</td><td>sgenet-1</td><td>KYN-PUBLIC 🟢</td><td>2749270</td><td>2348001</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T03:20:27.662631648UTC</td></tr><tr><td>65.109.118.169:46657</td><td>sgenet-1</td><td>jayjayservice 🟢</td><td>2749273</td><td>2456001</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T03:20:44.537996805UTC</td></tr><tr><td>65.108.41.177:43422</td><td>sgenet-1</td><td>STAVR_guide 🔴</td><td>2749273</td><td>2692001</td><td>False</td><td>off</td><td>15</td><td>2024-03-12T03:20:45.101390911UTC</td></tr><tr><td>135.181.210.171:1157</td><td>sgenet-1</td><td>STAVR-Service 🟢</td><td>2749276</td><td>2747001</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T03:21:12.107329537UTC</td></tr></table>
