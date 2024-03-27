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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>11200163</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:19:00.839987601UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>11200171</td><td>8262001</td><td>False</td><td>off</td><td>38762234</td><td>2024-03-27T06:19:49.195096862UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>11200129</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:15:32.738269680UTC</td></tr><tr><td>65.108.232.181:1111</td><td>umee-1</td><td>STAVRguide 🟢</td><td>11177300</td><td>10560001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:15:20.116841620UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>11200171</td><td>10691018</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:19:49.528234210UTC</td></tr><tr><td>65.108.73.245:26657</td><td>umee-1</td><td>tienthuattoan 🟢</td><td>11200151</td><td>10787155</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:17:48.127539665UTC</td></tr><tr><td>161.97.96.91:11657</td><td>umee-1</td><td>ams-rpc 🟢</td><td>11200181</td><td>10929930</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:20:44.112057939UTC</td></tr><tr><td>23.92.76.110:26657</td><td>umee-1</td><td>node 🟢</td><td>11200190</td><td>10938001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:21:41.695788907UTC</td></tr><tr><td>168.119.10.134:26664</td><td>umee-1</td><td>TrustedPoint 🟢</td><td>11200153</td><td>10998445</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:17:56.728604703UTC</td></tr><tr><td>37.60.244.38:26657</td><td>umee-1</td><td>iptraderpc 🟢</td><td>11177300</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:16:17.861003212UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>11200144</td><td>11013104</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:17:05.755511814UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>11200142</td><td>11029001</td><td>False</td><td>on</td><td>35123635</td><td>2024-03-27T06:16:53.100490665UTC</td></tr><tr><td>195.201.130.235:26657</td><td>umee-1</td><td>PRO-NODES75-RPC 🟢</td><td>11200161</td><td>11100161</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:18:50.206066920UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>11200181</td><td>11100181</td><td>False</td><td>off</td><td>38515018</td><td>2024-03-27T06:20:43.863559055UTC</td></tr><tr><td>142.132.215.124:11057</td><td>umee-1</td><td>StakeVillage 🟢</td><td>11200189</td><td>11177889</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T06:21:32.598833127UTC</td></tr><tr><td>116.202.192.143:60717</td><td>umee-1</td><td>VU 🟢</td><td>11200133</td><td>11193001</td><td>False</td><td>off</td><td>0</td><td>2024-03-27T06:15:58.545544042UTC</td></tr><tr><td>128.199.110.44:26657</td><td>umee-1</td><td>snap 🟢</td><td>11200179</td><td>11199964</td><td>False</td><td>off</td><td>0</td><td>2024-03-27T06:20:35.080614934UTC</td></tr></table>
