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

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER-M🔥:    https://explorer.stavr.tech/Andromeda-Mainnet            `Indexer "ON"` \
🔥API-M🔥:         https://andro.api.m.stavr.tech \
🔥RPC-M🔥:         https://andro.rpc.m.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC-M🔥:        http://andro.grpc.m.stavr.tech:132 \
🔥peer-M🔥:        `e4c2267b90c7cfbb45090ab7647dc01df97f58f9@andromeda-m.peer.stavr.tech:4376` \
🔥WASM-M🔥: updated every 2 hours `curl -o - -L http://andro.wasm.stavr.tech:1017/wasm-andromeda.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromeda --strip-components 2` \
🔥Genesis-M🔥: `wget -O $HOME/.andromeda/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/genesis.json"` \
🔥Addrbook-M🔥: `wget -O $HOME/.andromeda/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"` \
🔥Auto_install script-T🔥: `wget -O adprotocol https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/Testnet/adprotocol && chmod +x adprotocol && ./adprotocol` \

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/AndromedaProtocol/Decentralization)🔥
=

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

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.238.215:27357</td><td>andromeda-1</td><td>CroutonDigital 🟢</td><td>1343155</td><td>756001</td><td>False</td><td>on</td><td>0</td><td>2024-02-23T10:27:53.445891288UTC</td></tr><tr><td>5.189.151.202:26677</td><td>andromeda-1</td><td>AVIAONE 🟢</td><td>1343159</td><td>911001</td><td>False</td><td>on</td><td>0</td><td>2024-02-23T10:28:17.776319164UTC</td></tr><tr><td>132.145.205.66:26657</td><td>andromeda-1</td><td>InfStones 🟢</td><td>1343159</td><td>1299250</td><td>False</td><td>on</td><td>0</td><td>2024-02-23T10:28:15.206375329UTC</td></tr><tr><td>135.181.210.171:4137</td><td>andromeda-1</td><td>STAVR-Service 🟢</td><td>1343156</td><td>1340401</td><td>False</td><td>on</td><td>0</td><td>2024-02-23T10:27:55.815052152UTC</td></tr></table>
