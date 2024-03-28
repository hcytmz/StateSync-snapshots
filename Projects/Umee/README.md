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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>94.130.52.123:26657</td><td>umee-1</td><td>ELYSIUM 🔴</td><td>11212919</td><td>3216011</td><td>False</td><td>on</td><td>23244658</td><td>2024-03-28T03:32:01.242275030UTC</td></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>11212911</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:31:10.950788067UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>11212919</td><td>8262001</td><td>False</td><td>off</td><td>38762754</td><td>2024-03-28T03:32:00.962537940UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>11212879</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:27:57.132810442UTC</td></tr><tr><td>148.251.88.145:10257</td><td>umee-1</td><td>node 🟢</td><td>11212891</td><td>10179652</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:29:09.190501632UTC</td></tr><tr><td>65.108.232.181:1111</td><td>umee-1</td><td>STAVRguide 🟢</td><td>11177300</td><td>10560001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:27:40.465648540UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>11212919</td><td>10691018</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:32:01.477000725UTC</td></tr><tr><td>65.108.73.245:26657</td><td>umee-1</td><td>tienthuattoan 🟢</td><td>11212900</td><td>10787155</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:30:06.571749695UTC</td></tr><tr><td>161.97.96.91:11657</td><td>umee-1</td><td>ams-rpc 🟢</td><td>11212929</td><td>10929930</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:32:55.877668025UTC</td></tr><tr><td>23.92.76.110:26657</td><td>umee-1</td><td>node 🟢</td><td>11212938</td><td>10938001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:33:55.287818007UTC</td></tr><tr><td>37.60.244.38:26657</td><td>umee-1</td><td>iptraderpc 🟢</td><td>11177300</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:28:40.416062071UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>11212893</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:29:26.277762062UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>11212891</td><td>11029001</td><td>False</td><td>on</td><td>35123642</td><td>2024-03-28T03:29:13.581356671UTC</td></tr><tr><td>195.201.130.235:26657</td><td>umee-1</td><td>PRO-NODES75-RPC 🟢</td><td>11212910</td><td>11112910</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:31:02.581633281UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>11212928</td><td>11112928</td><td>False</td><td>off</td><td>38515534</td><td>2024-03-28T03:32:55.617703592UTC</td></tr><tr><td>142.132.215.124:11057</td><td>umee-1</td><td>StakeVillage 🔴</td><td>11212937</td><td>11177889</td><td>False</td><td>on</td><td>1761915</td><td>2024-03-28T03:33:46.177458287UTC</td></tr><tr><td>116.202.192.143:60717</td><td>umee-1</td><td>VU 🟢</td><td>11212883</td><td>11193001</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T03:28:22.963659075UTC</td></tr><tr><td>135.181.210.171:10457</td><td>umee-1</td><td>STAVR-Service 🟢</td><td>11212922</td><td>11210001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T03:32:16.334130229UTC</td></tr><tr><td>128.199.110.44:26657</td><td>umee-1</td><td>snap 🟢</td><td>11212926</td><td>11210784</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T03:32:42.731743213UTC</td></tr></table>
