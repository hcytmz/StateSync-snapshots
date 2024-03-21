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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>94.130.52.123:26657</td><td>umee-1</td><td>ELYSIUM 🔴</td><td>11111557</td><td>3216011</td><td>False</td><td>on</td><td>23232871</td><td>2024-03-21T02:46:26.600873724UTC</td></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>11111549</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:45:36.071996617UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>11111557</td><td>8262001</td><td>False</td><td>off</td><td>38787849</td><td>2024-03-21T02:46:26.314730933UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>11111513</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:42:05.203864766UTC</td></tr><tr><td>142.132.215.124:11057</td><td>umee-1</td><td>StakeVillage 🔴</td><td>11111576</td><td>10027726</td><td>False</td><td>on</td><td>1757783</td><td>2024-03-21T02:48:21.863054064UTC</td></tr><tr><td>148.251.88.145:10257</td><td>umee-1</td><td>node 🟢</td><td>11111526</td><td>10179652</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:43:21.812709357UTC</td></tr><tr><td>65.108.232.181:1111</td><td>umee-1</td><td>STAVRguide 🟢</td><td>11111511</td><td>10560001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:41:48.550050204UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>11111557</td><td>10691018</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:46:28.892096912UTC</td></tr><tr><td>135.181.229.110:27657</td><td>umee-1</td><td>rpc 🟢</td><td>11111522</td><td>10754071</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:42:54.897198017UTC</td></tr><tr><td>65.108.73.245:26657</td><td>umee-1</td><td>tienthuattoan 🟢</td><td>11111536</td><td>10787155</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:44:22.793314686UTC</td></tr><tr><td>161.97.96.91:11657</td><td>umee-1</td><td>ams-rpc 🟢</td><td>11111568</td><td>10929930</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:47:33.266726542UTC</td></tr><tr><td>168.119.10.134:26664</td><td>umee-1</td><td>TrustedPoint 🟢</td><td>11111537</td><td>10998445</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:44:29.300392734UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>11111568</td><td>11011568</td><td>False</td><td>off</td><td>38530554</td><td>2024-03-21T02:47:33.014799856UTC</td></tr><tr><td>37.60.244.38:26657</td><td>umee-1</td><td>iptraderpc 🟢</td><td>11111521</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:42:50.404007301UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>11111523</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:43:36.699577643UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>11111526</td><td>11029001</td><td>False</td><td>on</td><td>35123627</td><td>2024-03-21T02:43:24.169419885UTC</td></tr><tr><td>116.202.192.143:60717</td><td>umee-1</td><td>VU 🟢</td><td>11111518</td><td>11042001</td><td>False</td><td>off</td><td>0</td><td>2024-03-21T02:42:30.779035057UTC</td></tr><tr><td>195.201.130.235:26657</td><td>umee-1</td><td>PRO-NODES75-RPC 🟢</td><td>11111546</td><td>11071831</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:45:23.441724181UTC</td></tr><tr><td>95.165.150.165:26657</td><td>umee-1</td><td>SUNREN_RPC 🟢</td><td>11111568</td><td>11086378</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T02:47:32.666670235UTC</td></tr><tr><td>128.199.110.44:26657</td><td>umee-1</td><td>snap 🟢</td><td>11111565</td><td>11109878</td><td>False</td><td>off</td><td>0</td><td>2024-03-21T02:47:17.690261037UTC</td></tr></table>
