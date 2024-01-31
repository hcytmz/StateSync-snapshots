<h1 align="center"> 🔥Crescent Network🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Crescent)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
cd $HOME
SNAP_RPC=https://crescent.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.crescent/config/config.toml
crescentd tendermint unsafe-reset-all
wget -O $HOME/.crescent/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crescent/addrbook.json"
sudo systemctl restart crescentd && sudo journalctl -u crescentd -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop crescentd
cp $HOME/.crescent/data/priv_validator_state.json $HOME/.crescent/priv_validator_state.json.backup
rm -rf $HOME/.crescent/data
curl -o - -L https://crescent.snapshot.stavr.tech/crescent/crescent-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.crescent --strip-components 2
mv $HOME/.crescent/priv_validator_state.json.backup $HOME/.crescent/data/priv_validator_state.json
wget -O $HOME/.crescent/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crescent/addrbook.json"
sudo systemctl restart crescentd && journalctl -u crescentd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Crescent-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://crescent.api.m.stavr.tech \
🔥RPC🔥:          https://crescent.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://crescent.grpc.m.stavr.tech:106 \
🔥seed🔥:      `9145f046846e4f6121885903f21c47f6ca3e747e@crescent.seed.stavr.tech:2046` \
🔥Addrbook🔥:  `wget -O $HOME/.crescent/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crescent/addrbook.json"` \
🔥Auto_install script🔥:`wget -O crescentm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crescent/crescentm && chmod +x crescentm && ./crescentm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Crescnet/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.crescentm.stavr.tech/crescentm/rpc-crescentm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>148.251.246.239:28005</td><td>crescent-1</td><td>crescent-node 🟢</td><td>10750491</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-31T12:04:50.925503653UTC</td></tr><tr><td>188.172.228.225:26657</td><td>crescent-1</td><td>YTWOFUND_PEREFMAIN 🟢</td><td>10750497</td><td>6160001</td><td>False</td><td>on</td><td>0</td><td>2024-01-31T12:05:24.060434304UTC</td></tr><tr><td>148.251.8.22:26457</td><td>crescent-1</td><td>crescent_rpc 🟢</td><td>10750503</td><td>10548903</td><td>False</td><td>on</td><td>0</td><td>2024-01-31T12:05:57.744245192UTC</td></tr><tr><td>66.45.246.166:2037</td><td>crescent-1</td><td>STAVR-Service 🟢</td><td>10750501</td><td>10746001</td><td>False</td><td>on</td><td>0</td><td>2024-01-31T12:05:45.188758775UTC</td></tr></table>