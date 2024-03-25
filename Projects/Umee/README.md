<h1 align="center"> 🔥Umee🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Umee)
=
# StateSync Umee
```python
SNAP_RPC=https://umee.rpc.m.stavr.tech:443
peers="cb24fcba3bdbf867a495d4a1c78224603bcb558b@umee.peers.m.stavr.tech:10456"
sed -i -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.umee/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.umee/config/config.toml
umeed tendermint unsafe-reset-all --home $HOME/.umee
wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop umeed
cp $HOME/.umee/data/priv_validator_state.json $HOME/.umee/priv_validator_state.json.backup
rm -rf $HOME/.umee/data
curl -o - -L http://umee.snapshot.stavr.tech:1000/umee/umee-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.umee --strip-components 2
wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"
mv $HOME/.umee/priv_validator_state.json.backup $HOME/.umee/data/priv_validator_state.json
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Umee/staking             `Indexer "ON"` \
🔥EXPLORER Testnet🔥:        https://explorer.stavr.tech/umee-canon/staking      `Indexer "ON"` \
🔥API Mainnet🔥:                   https://umee.api.m.stavr.tech \
🔥API Testnet🔥:                     https://umee.api.t.stavr.tech \
🔥RPC🔥:                           https://umee.rpc.m.stavr.tech:443                     `Snapshot-interval = 300` \
🔥gRPC🔥:                              http://umee.grpc.m.stavr.tech:1190 \
🔥peer🔥:                     `cb24fcba3bdbf867a495d4a1c78224603bcb558b@umee.peers.m.stavr.tech:10456` \
🔥Addrbook🔥:    ```wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O Ume https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/Ume && chmod +x Ume && ./Ume```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Umee/Decentralization)🔥
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

[raw json Mainnet](https://rpc-check.umeem.stavr.tech/umeem/rpc-umeem-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>11172535</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:59:07.911223316UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>11172544</td><td>8262001</td><td>False</td><td>off</td><td>38782127</td><td>2024-03-25T08:00:00.089775173UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>11172502</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:55:48.538266370UTC</td></tr><tr><td>142.132.215.124:11057</td><td>umee-1</td><td>StakeVillage 🔴</td><td>11172563</td><td>10027726</td><td>False</td><td>on</td><td>1760636</td><td>2024-03-25T08:01:52.812645767UTC</td></tr><tr><td>148.251.88.145:10257</td><td>umee-1</td><td>node 🟢</td><td>11172515</td><td>10179652</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:57:05.668424994UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>11172544</td><td>10691018</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T08:00:02.468504803UTC</td></tr><tr><td>135.181.229.110:27657</td><td>umee-1</td><td>rpc 🟢</td><td>11172510</td><td>10754071</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:56:40.759777985UTC</td></tr><tr><td>65.108.73.245:26657</td><td>umee-1</td><td>tienthuattoan 🟢</td><td>11172524</td><td>10787155</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:58:03.097514345UTC</td></tr><tr><td>65.21.91.99:16857</td><td>umee-1</td><td>Staketab-snapshot 🟢</td><td>11172526</td><td>10910001</td><td>False</td><td>off</td><td>0</td><td>2024-03-25T07:58:11.653179196UTC</td></tr><tr><td>161.97.96.91:11657</td><td>umee-1</td><td>ams-rpc 🟢</td><td>11172555</td><td>10929930</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T08:01:04.694475537UTC</td></tr><tr><td>23.92.76.110:26657</td><td>umee-1</td><td>node 🟢</td><td>11172564</td><td>10938001</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T08:01:59.858290507UTC</td></tr><tr><td>37.60.244.38:26657</td><td>umee-1</td><td>iptraderpc 🟢</td><td>11172510</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:56:38.310545753UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>11172517</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:57:22.729544909UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>11172515</td><td>11029001</td><td>False</td><td>on</td><td>35123635</td><td>2024-03-25T07:57:08.001722939UTC</td></tr><tr><td>116.202.192.143:60717</td><td>umee-1</td><td>VU 🟢</td><td>11172506</td><td>11042001</td><td>False</td><td>off</td><td>0</td><td>2024-03-25T07:56:16.440474102UTC</td></tr><tr><td>195.201.130.235:26657</td><td>umee-1</td><td>PRO-NODES75-RPC 🟢</td><td>11172533</td><td>11072533</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T07:58:57.301481873UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>11172555</td><td>11072555</td><td>False</td><td>off</td><td>38534808</td><td>2024-03-25T08:01:04.427931012UTC</td></tr><tr><td>135.181.210.171:10457</td><td>umee-1</td><td>STAVR-Service 🟢</td><td>11172548</td><td>11169001</td><td>False</td><td>on</td><td>0</td><td>2024-03-25T08:00:23.454523024UTC</td></tr><tr><td>128.199.110.44:26657</td><td>umee-1</td><td>snap 🟢</td><td>11172553</td><td>11171325</td><td>False</td><td>off</td><td>0</td><td>2024-03-25T08:00:51.492994647UTC</td></tr></table>
