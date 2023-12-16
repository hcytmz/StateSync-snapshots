<h1 align="center"> 🔥Shentu🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Shentu)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://shentu.rpc.m.stavr.tech:20017
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
🔥RPC🔥:          http://shentu.rpc.m.stavr.tech:20017              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://shentu.grpc.m.stavr.tech:9593 \
🔥peer🔥:         `060027d3bc10ff7ebc1ec315ae5671c541e1568c@shentu.peer.stavr.tech:20016` \
🔥Addrbook🔥:  `wget -O $HOME/.shentud/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.shentud/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/genesis.json"` \
🔥Auto_install script🔥:`wget -O shentum https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Shentu/shentum && chmod +x shentum && ./shentum`

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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>3.219.242.171:26657</td><td>shentu-2.2</td><td>oracle_node 🟢</td><td>16344156</td><td>7515201</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:13:11.183805827UTC</td></tr><tr><td>35.153.156.23:26657</td><td>shentu-2.2</td><td>oracle_node 🟢</td><td>16344163</td><td>7515201</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:13:57.353146400UTC</td></tr><tr><td>35.74.10.164:6657</td><td>shentu-2.2</td><td>StakeBowlNode 🔴</td><td>16344156</td><td>8308501</td><td>False</td><td>on</td><td>50178</td><td>2023-12-16T11:13:15.034531231UTC</td></tr><tr><td>44.192.97.59:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16344156</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:13:13.853047828UTC</td></tr><tr><td>44.203.246.233:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16344158</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:13:23.809277302UTC</td></tr><tr><td>3.237.179.245:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16344159</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:13:32.701648819UTC</td></tr><tr><td>3.238.157.164:26657</td><td>shentu-2.2</td><td>indexer 🟢</td><td>16344161</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:13:42.000900670UTC</td></tr><tr><td>35.75.32.253:6657</td><td>shentu-2.2</td><td>StakeBowlFullNode 🟢</td><td>16344165</td><td>10470762</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:14:05.041033983UTC</td></tr><tr><td>165.232.72.33:26657</td><td>shentu-2.2</td><td>SuperNova 🟢</td><td>16344165</td><td>15936001</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:14:03.821922807UTC</td></tr><tr><td>142.132.202.86:56657</td><td>shentu-2.2</td><td>ramuchi.tech 🟢</td><td>16344171</td><td>16196001</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:14:40.488664905UTC</td></tr><tr><td>144.91.65.13:26687</td><td>shentu-2.2</td><td>AviaBloc_by_AviaOne 🟢</td><td>16344166</td><td>16335299</td><td>False</td><td>off</td><td>0</td><td>2023-12-16T11:14:13.534612384UTC</td></tr><tr><td>66.45.246.166:20017</td><td>shentu-2.2</td><td>STAVR-Service 🟢</td><td>16344171</td><td>16342501</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T11:14:45.194113064UTC</td></tr></table>
