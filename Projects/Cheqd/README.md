<h1 align="center"> 🔥CHEQD🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Cheqd)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://cheqd.rpc.m.stavr.tech:26337
SEEDS=46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016
cp $HOME/.cheqdnode/data/priv_validator_state.json $HOME/.cheqdnode/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.cheqdnode/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.cheqdnode/config/config.toml
cheqd-noded tendermint unsafe-reset-all --home $HOME/.cheqdnode --keep-addr-book
mv $HOME/.cheqdnode/priv_validator_state.json.backup $HOME/.cheqdnode/data/priv_validator_state.json
sudo systemctl restart cheqd-noded && journalctl -u cheqd-noded -f -o cat
```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop cheqd-noded
cp $HOME/.cheqdnode/data/priv_validator_state.json $HOME/.cheqdnode/priv_validator_state.json.backup
rm -rf $HOME/.cheqdnode/data
curl -o - -L http://cheqd.snapshot.stavr.tech:4/cheqd/cheqd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.cheqdnode --strip-components 2
mv $HOME/.cheqdnode/priv_validator_state.json.backup $HOME/.cheqdnode/data/priv_validator_state.json
wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"
sudo systemctl restart cheqd-noded && journalctl -u cheqd-noded -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Cheqd-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://cheqd.api.m.stavr.tech \
🔥RPC🔥:          http://cheqd.rpc.m.stavr.tech:26337              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://cheqd.grpc.m.stavr.tech:9337 \
🔥peer🔥:         `46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016` \
🔥Addrbook🔥:  `wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.cheqdnode/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/genesis.json"` \
🔥Auto_install script🔥:`wget -O cheqdm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/cheqdm && chmod +x cheqdm && ./cheqdm`

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

[raw Mainnet json](https://rpc-check.cheqdm.stavr.tech/cheqdm/rpc-cheqdm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>3.219.242.171:26657</td><td>shentu-2.2</td><td>oracle_node 🟢</td><td>16168511</td><td>7515201</td><td>False</td><td>0</td><td>2023-12-04T09:55:08.054088958UTC</td></tr><tr><td>35.153.156.23:26657</td><td>shentu-2.2</td><td>oracle_node 🟢</td><td>16168519</td><td>7515201</td><td>False</td><td>0</td><td>2023-12-04T09:55:54.530451978UTC</td></tr><tr><td>35.74.10.164:6657</td><td>shentu-2.2</td><td>StakeBowlNode 🔴</td><td>16168512</td><td>8308501</td><td>False</td><td>50178</td><td>2023-12-04T09:55:14.030145910UTC</td></tr><tr><td>44.192.97.59:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16168512</td><td>9786901</td><td>False</td><td>0</td><td>2023-12-04T09:55:12.747348920UTC</td></tr><tr><td>44.203.246.233:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16168513</td><td>9786901</td><td>False</td><td>0</td><td>2023-12-04T09:55:20.770277904UTC</td></tr><tr><td>3.237.179.245:26657</td><td>shentu-2.2</td><td>full 🟢</td><td>16168515</td><td>9786901</td><td>False</td><td>0</td><td>2023-12-04T09:55:29.770034421UTC</td></tr><tr><td>3.238.157.164:26657</td><td>shentu-2.2</td><td>indexer 🟢</td><td>16168517</td><td>9786901</td><td>False</td><td>0</td><td>2023-12-04T09:55:41.178486066UTC</td></tr><tr><td>35.75.32.253:6657</td><td>shentu-2.2</td><td>StakeBowlFullNode 🟢</td><td>16168521</td><td>10470762</td><td>False</td><td>0</td><td>2023-12-04T09:56:04.341563819UTC</td></tr><tr><td>142.132.202.86:56657</td><td>shentu-2.2</td><td>ramuchi.tech 🟢</td><td>16168527</td><td>15224001</td><td>False</td><td>0</td><td>2023-12-04T09:56:39.887572908UTC</td></tr><tr><td>165.232.72.33:26657</td><td>shentu-2.2</td><td>SuperNova 🟢</td><td>16168520</td><td>15936001</td><td>False</td><td>0</td><td>2023-12-04T09:56:03.031746797UTC</td></tr><tr><td>192.99.160.197:22657</td><td>shentu-2.2</td><td>KYN-SIDE 🟢</td><td>16139910</td><td>16083091</td><td>False</td><td>0</td><td>2023-12-04T09:56:45.427399453UTC</td></tr><tr><td>185.162.249.161:30657</td><td>shentu-2.2</td><td>tienthuattoan 🟢</td><td>16161110</td><td>16084527</td><td>False</td><td>0</td><td>2023-12-04T09:55:47.779637966UTC</td></tr><tr><td>144.91.65.13:26687</td><td>shentu-2.2</td><td>AviaBloc_by_AviaOne 🟢</td><td>16168521</td><td>16160503</td><td>False</td><td>0</td><td>2023-12-04T09:56:10.826698366UTC</td></tr></table>
