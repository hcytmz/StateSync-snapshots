  <h1 align="center"> 🔥Lava🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Lava_Network)
=

<h1 align="center"> TESTNET</h1>

# StateSync Lava Testnet
```python
SNAP_RPC=https://lava.rpc.t.stavr.tech:443
peers="46a02fc2908aec60985fd2852c424907d6f79ed7@lava.peers.stavr.tech:197"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.lava/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.lava/config/config.toml
lavad tendermint unsafe-reset-all --home /root/.lava --keep-addr-book
systemctl restart lavad && journalctl -u lavad -f -o cat
```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop lavad
cp $HOME/.lava/data/priv_validator_state.json $HOME/.lava/priv_validator_state.json.backup
rm -rf $HOME/.lava/data
curl -o - -L http://lava.snapshot.stavr.tech:1020/lava/lava-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lava --strip-components 2
mv $HOME/.lava/priv_validator_state.json.backup $HOME/.lava/data/priv_validator_state.json
wget -O $HOME/.lava/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lava_Network/addrbook.json"
sudo systemctl restart lavad && journalctl -u lavad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Lava-Testnet/staking        `Indexer "ON"` \
🔥API🔥:      https://lava.api.t.stavr.tech \
🔥RPC🔥:      https://lava.rpc.t.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC🔥:     http://lava.grpc.t.stavr.tech:179 \
🔥peer🔥:     `46a02fc2908aec60985fd2852c424907d6f79ed7@lava.peers.stavr.tech:197` \
🔥Genesis🔥:  ```curl -s https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lava_Network/genesis.json > $HOME/.lava/config/genesis.json``` \
🔥Addrbook🔥: ```wget -O $HOME/.lava/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lava_Network/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O lav https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lava_Network/lav && chmod +x lav && ./lav`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Lava/Decentralization)🔥
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

[raw json Testnet](https://rpc-check.lavat.stavr.tech/lavat/rpc-lavat-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>976637</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:41.800437347UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:52.366231159UTC</td></tr><tr><td>195.201.164.54:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>976638</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:59.283956951UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:12.807856053UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>976639</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-27T19:20:16.556144589UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:17.000279342UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>976640</td><td>340778</td><td>False</td><td>off</td><td>1200958391</td><td>2024-03-27T19:20:25.037764539UTC</td></tr><tr><td>185.196.20.78:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>881586</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:25.336371729UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>976642</td><td>340778</td><td>False</td><td>on</td><td>11976722</td><td>2024-03-27T19:21:09.139964449UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:23.332725763UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>976642</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:25.624463758UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:25.889942899UTC</td></tr><tr><td>167.86.85.35:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926699</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:43.417489982UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:46.872438244UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:54.276137202UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>975158</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:56.635535266UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:23.016382764UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>976642</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-27T19:21:11.962345676UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:16.779937560UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>976638</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-27T19:19:55.284415183UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>976638</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:59.618364264UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>976644</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-27T19:21:43.968686105UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>976645</td><td>751501</td><td>False</td><td>on</td><td>10104218</td><td>2024-03-27T19:21:51.978453228UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>976638</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-27T19:20:01.961181120UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:52.694249082UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>966391</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:47.407228947UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>976638</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:59.082644349UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>976639</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:17.291702195UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>975964</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:19.690571121UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>976631</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:19.937118105UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>966322</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:22.681409942UTC</td></tr><tr><td>109.199.112.157:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>976640</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:39.735419928UTC</td></tr><tr><td>15.165.182.226:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>975060</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:58.141858725UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-27T19:21:09.430608504UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>956967</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:38.785100013UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>976644</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:46.600212956UTC</td></tr><tr><td>109.199.97.128:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>976568</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:49.310326177UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>976632</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:51.623633777UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>976637</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-27T19:19:44.134497964UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>976637</td><td>862501</td><td>False</td><td>on</td><td>23408473</td><td>2024-03-27T19:19:49.746244489UTC</td></tr><tr><td>109.123.247.78:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:53.014496399UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:39.444733152UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>976637</td><td>876637</td><td>False</td><td>off</td><td>0</td><td>2024-03-27T19:19:50.064587492UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>976566</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:20:37.082747526UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>976636</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-27T19:19:39.184664875UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>976632</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:28.267443768UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>976638</td><td>955881</td><td>False</td><td>on</td><td>9950755</td><td>2024-03-27T19:19:57.678964625UTC</td></tr><tr><td>46.8.19.105:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>960053</td><td>960042</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:08.806296410UTC</td></tr><tr><td>91.207.54.126:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>970946</td><td>966001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:39.439742646UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>976640</td><td>970881</td><td>False</td><td>on</td><td>20286032</td><td>2024-03-27T19:20:27.576888809UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>976630</td><td>972301</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:19:46.445099128UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>976642</td><td>975001</td><td>False</td><td>on</td><td>0</td><td>2024-03-27T19:21:12.269938467UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>975661</td><td>975661</td><td>False</td><td>on</td><td>10415138</td><td>2024-03-27T19:19:58.865003634UTC</td></tr></table>
