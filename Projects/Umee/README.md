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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>11081111</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:14:36.247352219UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>11081115</td><td>8262001</td><td>False</td><td>off</td><td>38819389</td><td>2024-03-19T00:15:00.969724193UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>11081093</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:12:52.096583515UTC</td></tr><tr><td>142.132.215.124:11057</td><td>umee-1</td><td>StakeVillage 🔴</td><td>11081122</td><td>10027726</td><td>False</td><td>on</td><td>1756323</td><td>2024-03-19T00:15:42.093625807UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>11081115</td><td>10691018</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:15:01.258201765UTC</td></tr><tr><td>135.181.229.110:27657</td><td>umee-1</td><td>rpc 🟢</td><td>11081097</td><td>10754071</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:13:13.420153522UTC</td></tr><tr><td>65.108.73.245:26657</td><td>umee-1</td><td>tienthuattoan 🟢</td><td>11081106</td><td>10787155</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:14:05.185151752UTC</td></tr><tr><td>161.97.96.91:11657</td><td>umee-1</td><td>ams-rpc 🟢</td><td>11081119</td><td>10929930</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:15:23.574094618UTC</td></tr><tr><td>23.92.76.110:26657</td><td>umee-1</td><td>node 🟢</td><td>11081122</td><td>10938001</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:15:44.862826733UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>11081119</td><td>10981119</td><td>False</td><td>off</td><td>38561922</td><td>2024-03-19T00:15:23.306801997UTC</td></tr><tr><td>168.119.10.134:26664</td><td>umee-1</td><td>TrustedPoint 🟢</td><td>11081106</td><td>10998445</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:14:07.452525598UTC</td></tr><tr><td>37.60.244.38:26657</td><td>umee-1</td><td>iptraderpc 🟢</td><td>11081097</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:13:13.054467036UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>11081099</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:13:42.509376418UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>11081101</td><td>11029001</td><td>False</td><td>on</td><td>35123627</td><td>2024-03-19T00:13:36.118395184UTC</td></tr><tr><td>116.202.192.143:60717</td><td>umee-1</td><td>VU 🟢</td><td>11081095</td><td>11042001</td><td>False</td><td>off</td><td>0</td><td>2024-03-19T00:13:02.551773273UTC</td></tr><tr><td>135.181.210.171:10457</td><td>umee-1</td><td>STAVR-Service 🟢</td><td>11081116</td><td>11080001</td><td>False</td><td>on</td><td>0</td><td>2024-03-19T00:15:09.760440558UTC</td></tr><tr><td>128.199.110.44:26657</td><td>umee-1</td><td>snap 🟢</td><td>11081117</td><td>11080954</td><td>False</td><td>off</td><td>0</td><td>2024-03-19T00:15:16.844997231UTC</td></tr></table>
