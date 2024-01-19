<h1 align="center"> 🔥AndromedaProtocol Mainnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/AndromedaProtocol)
=

# StateSync Andromedad Mainnet
```python
SNAP_RPC=https://andro.rpc.m.stavr.tech:443
peers=e4c2267b90c7cfbb45090ab7647dc01df97f58f9@andromeda-m.peer.stavr.tech:4376
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.andromeda/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.andromeda/config/config.toml
andromedad tendermint unsafe-reset-all --home $HOME/.andromeda
systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
# SnapShot Mainnet (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop andromedad
cp $HOME/.andromeda/data/priv_validator_state.json $HOME/.andromeda/priv_validator_state.json.backup
rm -rf $HOME/.andromeda/data
curl -o - -L http://andro.snapshot.stavr.tech:1030/andromeda/andromeda-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2
curl -o - -L http://andro.wasm.stavr.tech:1017/wasm-andromeda.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2
mv $HOME/.andromeda/priv_validator_state.json.backup $HOME/.andromeda/data/priv_validator_state.json
wget -O $HOME/.andromeda/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"
sudo systemctl restart andromedad && journalctl -u andromedad -f -o cat
```


<h1 align="center"> 🔥AndromedaProtocol Testnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/AndromedaProtocol/Testnet)
=

# StateSync Andromedad Testnet (Temporarily disable)
```python
SNAP_RPC=http://andromedad.rpc.t.stavr.tech:4137
peers="d083506ef2e9d5f2ee22dabf4fa893a72e6cf483@andromedad.peer.stavr.tech:4376"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.andromedad/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.andromedad/config/config.toml
andromedad tendermint unsafe-reset-all --home $HOME/.andromedad
systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
# SnapShot Testnet (~0.5 GB) (Temporarily disable)
```python
cd $HOME
apt install lz4
sudo systemctl stop andromedad
cp $HOME/.andromedad/data/priv_validator_state.json $HOME/.andromedad/priv_validator_state.json.backup
rm -rf $HOME/.andromedad/data
curl -o - -L http://andromedad.snapshot.stavr.tech:1021/andromedad/andromedad-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2
curl -o - -L http://andromedad.wasm.stavr.tech:1002/wasm-andromedad.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2
mv $HOME/.andromedad/priv_validator_state.json.backup $HOME/.andromedad/data/priv_validator_state.json
wget -O $HOME/.andromedad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"
sudo systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER-M🔥:    https://explorer.stavr.tech/Andromeda-Mainnet            `Indexer "ON"` \
🔥EXPLORER-T🔥:    https://explorer.stavr.tech/Andromedad-testnet/staking            `Indexer "ON"` \
🔥API-M🔥:         https://andro.api.m.stavr.tech \
🔥API-T🔥:         https://andromedad.api.t.stavr.tech \
🔥RPC-M🔥:         https://andro.rpc.m.stavr.tech:443                  `Snapshot-interval = 100` \
🔥RPC-T🔥:         http://andromedad.rpc.t.stavr.tech:4137                  `Snapshot-interval = 100` \
🔥gRPC-M🔥:        http://andromedad.grpc.t.stavr.tech:132 \
🔥gRPC-T🔥:        http://andromedad.grpc.t.stavr.tech:11090 \
🔥peer-M🔥:        `e4c2267b90c7cfbb45090ab7647dc01df97f58f9@andromeda-m.peer.stavr.tech:4376` \
🔥peer-T🔥:        `d083506ef2e9d5f2ee22dabf4fa893a72e6cf483@andromedad.peer.stavr.tech:4376` \
🔥WASM-M🔥: updated every 2 hours `curl -o - -L http://andro.wasm.stavr.tech:1017/wasm-andromeda.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2` \
🔥WASM-T🔥: updated every 2 hours `curl -o - -L http://andromedad.wasm.stavr.tech:1002/wasm-andromedad.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2` \
🔥Genesis-M🔥: `wget -O $HOME/.andromeda/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/genesis.json"` \
🔥Genesis-T🔥: `wget -O $HOME/.andromedad/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/genesis.json"` \
🔥Addrbook-M🔥: `wget -O $HOME/.andromeda/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"` \
🔥Addrbook-T🔥: `wget -O $HOME/.andromedad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/addrbook.json"` \
🔥Auto_install script-T🔥: `wget -O adprotocol https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/adprotocol && chmod +x adprotocol && ./adprotocol` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/AndromedaProtocol/Decentralization)🔥

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

[raw Mainnet json](https://rpc-check.androm.stavr.tech/androm/rpc-androm-result.json) \
[raw Testnet json](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/AndromedaProtocol/Rpc-Check-Testnet)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.189.151.202:26677</td><td>andromeda-1</td><td>AVIAONE 🟢</td><td>833270</td><td>822001</td><td>False</td><td>on</td><td>0</td><td>2024-01-19T16:28:15.987423499UTC</td></tr><tr><td>135.181.210.171:4137</td><td>andromeda-1</td><td>STAVR-Service 🟢</td><td>833267</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-01-19T16:27:58.063302933UTC</td></tr></table>
