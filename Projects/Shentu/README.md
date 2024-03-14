<h1 align="center"> 🔥Shentu🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Shentu)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://shentu.rpc.m.stavr.tech:443
SEEDS=060027d3bc10ff7ebc1ec315ae5671c541e1568c@shentu.peer.stavr.tech:20016
cp $HOME/.shentud/data/priv_validator_state.json $HOME/.shentud/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.shentud/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.shentud/config/config.toml
shentud tendermint unsafe-reset-all --home $HOME/.shentud --keep-addr-book
mv $HOME/.shentud/priv_validator_state.json.backup $HOME/.shentud/data/priv_validator_state.json
sudo systemctl restart shentud && journalctl -u shentud -f -o cat
```
# SnapShot (~3 GB) updated every 7 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop shentud
cp $HOME/.shentud/data/priv_validator_state.json $HOME/.shentud/priv_validator_state.json.backup
rm -rf $HOME/.shentud/data
curl -o - -L http://shentu.snapshot.stavr.tech:2/shentud/shentud-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.shentud --strip-components 2
mv $HOME/.shentud/priv_validator_state.json.backup $HOME/.shentud/data/priv_validator_state.json
wget -O $HOME/.shentud/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/addrbook.json"
sudo systemctl restart shentud && journalctl -u shentud -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Shentu-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://shentu.api.m.stavr.tech \
🔥RPC🔥:          https://shentu.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://shentu.grpc.m.stavr.tech:9593 \
🔥peer🔥:         `060027d3bc10ff7ebc1ec315ae5671c541e1568c@shentu.peer.stavr.tech:20016` \
🔥Addrbook🔥:  `wget -O $HOME/.shentud/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.shentud/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/genesis.json"` \
🔥Auto_install script🔥:`wget -O shentum https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/shentum && chmod +x shentum && ./shentum`

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

[raw Mainnet json](https://rpc-check.shentum.stavr.tech/shentum/rpc-shentum-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>35.74.10.164:6657</td><td>shentu-2.2</td><td>StakeBowlNode 🔴</td><td>17626089</td><td>8308501</td><td>False</td><td>on</td><td>50178</td><td>2024-03-14T01:48:23.833160625UTC</td></tr><tr><td>44.192.97.59:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>17626088</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:48:20.506697986UTC</td></tr><tr><td>44.203.246.233:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>17626090</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:48:32.605932701UTC</td></tr><tr><td>3.237.179.245:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>17626092</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:48:41.381803293UTC</td></tr><tr><td>3.238.157.164:26657</td><td>shentu-2.2</td><td>indexer 🟢</td><td>17626094</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:48:52.621205357UTC</td></tr><tr><td>35.75.32.253:6657</td><td>shentu-2.2</td><td>StakeBowlFullNode 🟢</td><td>17626098</td><td>10470762</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:49:16.842985066UTC</td></tr><tr><td>165.232.72.33:26657</td><td>shentu-2.2</td><td>SuperNova 🟢</td><td>17626098</td><td>15936001</td><td>False</td><td>off</td><td>0</td><td>2024-03-14T01:49:15.552919202UTC</td></tr><tr><td>142.132.202.86:56657</td><td>shentu-2.2</td><td>ramuchi.tech 🟢</td><td>17626105</td><td>16196001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:49:55.346261260UTC</td></tr><tr><td>65.109.94.26:26657</td><td>shentu-2.2</td><td>bricks 🟢</td><td>17626106</td><td>16401001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:50:02.313384601UTC</td></tr><tr><td>65.108.44.124:26657</td><td>shentu-2.2</td><td>bricks 🟢</td><td>17626106</td><td>16401001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:50:06.682914535UTC</td></tr><tr><td>158.69.27.233:23657</td><td>shentu-2.2</td><td>KYN-RPC 🟢</td><td>17528125</td><td>16778677</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:49:53.098745219UTC</td></tr><tr><td>95.165.89.222:25657</td><td>shentu-2.2</td><td>Max_Foton_nodes 🔴</td><td>17626100</td><td>17144052</td><td>False</td><td>on</td><td>2408</td><td>2024-03-14T01:49:27.737889009UTC</td></tr><tr><td>65.108.73.245:28657</td><td>shentu-2.2</td><td>tienthuattoan 🟢</td><td>17415110</td><td>17399930</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:49:28.035889729UTC</td></tr><tr><td>66.45.246.166:20017</td><td>shentu-2.2</td><td>STAVR-Service 🟢</td><td>17626105</td><td>17619001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T01:50:01.988893648UTC</td></tr><tr><td>144.91.65.13:26687</td><td>shentu-2.2</td><td>AviaBloc_by_AviaOne 🟢</td><td>17626099</td><td>17622963</td><td>False</td><td>off</td><td>0</td><td>2024-03-14T01:49:25.328804540UTC</td></tr></table>
