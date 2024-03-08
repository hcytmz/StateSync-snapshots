<h1 align="center"> 🔥Chihuahua Chain🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Chihua)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://chihua.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.chihuahuad/config/config.toml
chihuahuad tendermint unsafe-reset-all
wget -O $HOME/.chihuahuad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Chihua/addrbook.json"
curl -o - -L https://chihua.wasm.stavr.tech/wasm-chihua.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.chihuahuad --strip-components 2
sudo systemctl restart chihuahuad && sudo journalctl -u chihuahuad -f -o cat
```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop chihuahuad
cp $HOME/.chihuahuad/data/priv_validator_state.json $HOME/.chihuahuad/priv_validator_state.json.backup
rm -rf $HOME/.chihuahuad/data
curl -o - -L https://chihua.snapshot.stavr.tech/chihua/chihua-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.chihuahuad --strip-components 2
mv $HOME/.chihuahuad/priv_validator_state.json.backup $HOME/.chihuahuad/data/priv_validator_state.json
wget -O $HOME/.chihuahuad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Chihua/addrbook.json"
sudo systemctl restart chihuahuad && journalctl -u chihuahuad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Chihua-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://chihua.api.m.stavr.tech \
🔥RPC🔥:          https://chihua.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://chihua.grpc.m.stavr.tech:108 \
🔥seed🔥:      `cd835cfc413755184239a3dcd24a1f9b5a98627b@chihua.seed.stavr.tech:2016` \
🔥Genesis🔥:   `wget -O $HOME/.chihuahuad/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Chihua/genesis.json"` \
🔥WASM🔥:      `curl -o - -L https://chihua.wasm.stavr.tech/wasm-chihua.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.chihuahuad --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.chihuahuad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Chihua/addrbook.json"` \
🔥Auto_install script🔥:`wget -O chihuam https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Chihua/chihuam && chmod +x chihuam && ./chihuam`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Chihua/Decentralization)🔥
=
<h1 align="center"> RPC Scanning</h1>

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

[raw Mainnet json](https://rpc-check.chihuam.stavr.tech/chihuam/rpc-chihuam-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>93.115.25.178:2011</td><td>chihuahua-1</td><td>Zenscape 🟢</td><td>11772865</td><td>9431588</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T02:46:17.673115811UTC</td></tr><tr><td>154.53.60.236:26657</td><td>chihuahua-1</td><td>xyz 🔴</td><td>11772852</td><td>10662121</td><td>False</td><td>off</td><td>111321624</td><td>2024-03-08T02:45:05.851011886UTC</td></tr><tr><td>66.172.36.140:56657</td><td>chihuahua-1</td><td>node 🟢</td><td>11772853</td><td>10925389</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T02:45:10.780548726UTC</td></tr><tr><td>66.172.36.139:56657</td><td>chihuahua-1</td><td>node 🟢</td><td>11772855</td><td>11512390</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T02:45:21.741773508UTC</td></tr></table>