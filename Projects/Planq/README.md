<h1 align="center"> 🔥PlanQ🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Planq)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://planq.rpc.m.stavr.tech:443
SEEDS=192ff55d15d7ad9fc9ded5c5a9f4393beba9b222@planq.peer.stavr.tech:1076
cp $HOME/.planqd/data/priv_validator_state.json $HOME/.planqd/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.planqd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.planqd/config/config.toml
planqd tendermint unsafe-reset-all --home $HOME/.planqd --keep-addr-book
mv $HOME/.planqd/priv_validator_state.json.backup $HOME/.planqd/data/priv_validator_state.json
sudo systemctl restart planqd && journalctl -u planqd -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop planqd
cp $HOME/.planqd/data/priv_validator_state.json $HOME/.planqd/priv_validator_state.json.backup
rm -rf $HOME/.planqd/data
curl -o - -L http://planq.snapshot.stavr.tech:8/planqd/planqd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.planqd --strip-components 2
mv $HOME/.planqd/priv_validator_state.json.backup $HOME/.planqd/data/priv_validator_state.json
wget -O $HOME/.planqd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Planq/addrbook.json"
sudo systemctl restart planqd && journalctl -u planqd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Planq-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://planq.api.m.stavr.tech \
🔥RPC🔥:          https://planq.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://planq.grpc.m.stavr.tech:2070 \
🔥peer🔥:         `192ff55d15d7ad9fc9ded5c5a9f4393beba9b222@planq.peer.stavr.tech:1076` \
🔥Addrbook🔥:  `wget -O $HOME/.planqd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Planq/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.planqd/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Planq/genesis.json"` \
🔥Auto_install script🔥:`wget -O planqm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Planq/planqm && chmod +x planqm && ./planqm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Planq/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.planqm.stavr.tech/planqm/rpc-planqm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.35.50:20357</td><td>planq_7070-2</td><td>893t-agagd-asgd8asdg-d 🟢</td><td>7516700</td><td>5067437</td><td>False</td><td>on</td><td>0</td><td>2024-03-11T16:46:51.255287562UTC</td></tr><tr><td>185.190.140.93:14657</td><td>planq_7070-2</td><td>geonodes 🔴</td><td>7894167</td><td>7650501</td><td>False</td><td>on</td><td>654047</td><td>2024-03-11T16:46:34.383522713UTC</td></tr><tr><td>65.108.66.174:31657</td><td>planq_7070-2</td><td>hello-BccNodesRPC 🟢</td><td>7894174</td><td>7650501</td><td>False</td><td>on</td><td>0</td><td>2024-03-11T16:47:11.041589405UTC</td></tr><tr><td>95.217.16.83:34657</td><td>planq_7070-2</td><td>MONIKER 🔴</td><td>7894170</td><td>7698001</td><td>False</td><td>on</td><td>427075</td><td>2024-03-11T16:46:50.970144193UTC</td></tr><tr><td>66.45.246.166:1077</td><td>planq_7070-2</td><td>STAVR-Service 🟢</td><td>7894172</td><td>7890001</td><td>False</td><td>on</td><td>0</td><td>2024-03-11T16:47:04.005898191UTC</td></tr><tr><td>192.99.160.197:13657</td><td>planq_7070-2</td><td>BACKUP_PLANQ 🟢</td><td>7891470</td><td>7890001</td><td>False</td><td>off</td><td>0</td><td>2024-03-11T16:47:04.612983499UTC</td></tr></table>
