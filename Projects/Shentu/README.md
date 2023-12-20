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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>35.74.10.164:6657</td><td>shentu-2.2</td><td>StakeBowlNode 🔴</td><td>16401115</td><td>8308501</td><td>False</td><td>on</td><td>50178</td><td>2023-12-20T08:54:37.492632407UTC</td></tr><tr><td>44.192.97.59:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16401115</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:54:36.202663698UTC</td></tr><tr><td>44.203.246.233:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16401116</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:54:46.311454768UTC</td></tr><tr><td>3.237.179.245:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16401118</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:54:55.217460886UTC</td></tr><tr><td>3.238.157.164:26657</td><td>shentu-2.2</td><td>indexer 🟢</td><td>16401120</td><td>9786901</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:55:06.597175833UTC</td></tr><tr><td>35.75.32.253:6657</td><td>shentu-2.2</td><td>StakeBowlFullNode 🟢</td><td>16401124</td><td>10470762</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:55:29.057510870UTC</td></tr><tr><td>165.232.72.33:26657</td><td>shentu-2.2</td><td>SuperNova 🟢</td><td>16401123</td><td>15936001</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:55:27.836798476UTC</td></tr><tr><td>192.99.160.197:22657</td><td>shentu-2.2</td><td>KYN-SIDE 🟢</td><td>16223540</td><td>16083091</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:56:01.786146208UTC</td></tr><tr><td>185.162.249.161:30657</td><td>shentu-2.2</td><td>tienthuattoan 🟢</td><td>16401110</td><td>16084527</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:55:13.197523686UTC</td></tr><tr><td>142.132.202.86:56657</td><td>shentu-2.2</td><td>ramuchi.tech 🟢</td><td>16401128</td><td>16196001</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:55:56.515078543UTC</td></tr><tr><td>144.91.65.13:26687</td><td>shentu-2.2</td><td>AviaBloc_by_AviaOne 🟢</td><td>16401125</td><td>16393637</td><td>False</td><td>off</td><td>0</td><td>2023-12-20T08:55:35.624269335UTC</td></tr><tr><td>66.45.246.166:20017</td><td>shentu-2.2</td><td>STAVR-Service 🟢</td><td>16401129</td><td>16395001</td><td>False</td><td>on</td><td>0</td><td>2023-12-20T08:55:59.112710797UTC</td></tr></table>
