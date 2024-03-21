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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>946627</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:25:52.984198404UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:03.385468786UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:28.124622872UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>946629</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-21T07:26:34.213983062UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:34.971629869UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>946630</td><td>340778</td><td>False</td><td>off</td><td>1200856881</td><td>2024-03-21T07:26:49.277608243UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>946631</td><td>340778</td><td>False</td><td>on</td><td>11976721</td><td>2024-03-21T07:27:38.021881366UTC</td></tr><tr><td>109.199.116.90:26657</td><td>lava-testnet-2</td><td>InkyaNode 🟢</td><td>931947</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:41.158590944UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:48.445662250UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>946632</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:50.741362867UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:51.060967261UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:19.518162449UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:31.775024634UTC</td></tr><tr><td>167.86.82.9:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926971</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:37.050844276UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>946635</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:39.886527279UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:48.146705726UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>946631</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-21T07:27:41.373882437UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:34.766048657UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>946627</td><td>714061</td><td>False</td><td>on</td><td>12712887</td><td>2024-03-21T07:26:06.262020065UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>946627</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:10.747721438UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>946633</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-21T07:28:11.276912697UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>946634</td><td>751501</td><td>False</td><td>on</td><td>10104218</td><td>2024-03-21T07:28:29.456653565UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>946627</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-21T07:26:15.121491115UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>946630</td><td>762001</td><td>False</td><td>on</td><td>21286031</td><td>2024-03-21T07:26:51.521320619UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>946627</td><td>764041</td><td>False</td><td>on</td><td>9950754</td><td>2024-03-21T07:26:08.690997896UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:03.699424636UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>946627</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:10.139344703UTC</td></tr><tr><td>31.220.94.180:26657</td><td>lava-testnet-2</td><td>EaVenture 🟢</td><td>946628</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:21.526586910UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>946628</td><td>833001</td><td>False</td><td>on</td><td>20047592</td><td>2024-03-21T07:26:21.736856324UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>946629</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:37.286663041UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>946628</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:39.635486538UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>946629</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:44.196685349UTC</td></tr><tr><td>109.199.112.157:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>946630</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:07.790223239UTC</td></tr><tr><td>15.165.182.226:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>946629</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:26.333060780UTC</td></tr><tr><td>154.53.48.19:14557</td><td>lava-testnet-2</td><td>Alisa 🟢</td><td>934687</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:33.032690377UTC</td></tr><tr><td>88.198.230.219:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>946631</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:37.699249797UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-21T07:27:38.320884737UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>946633</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:06.642832107UTC</td></tr><tr><td>161.97.76.144:26657</td><td>lava-testnet-2</td><td>f52y0u 🟢</td><td>946628</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:11.533990991UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>946633</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:15.928581763UTC</td></tr><tr><td>109.199.97.128:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>946634</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:23.972919317UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>946634</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:28:28.438620198UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>946627</td><td>846627</td><td>False</td><td>off</td><td>0</td><td>2024-03-21T07:26:01.054137149UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>946627</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-21T07:25:55.316394966UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>927794</td><td>859261</td><td>False</td><td>on</td><td>10520341</td><td>2024-03-21T07:26:09.900011600UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>946627</td><td>862501</td><td>False</td><td>on</td><td>23408471</td><td>2024-03-21T07:26:00.760883429UTC</td></tr><tr><td>93.159.130.38:28857</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>946632</td><td>862881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:51.369884995UTC</td></tr><tr><td>109.123.247.78:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:03.985896914UTC</td></tr><tr><td>84.46.255.1:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:10.442222693UTC</td></tr><tr><td>84.46.255.68:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:26:28.404895500UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:05.399293249UTC</td></tr><tr><td>89.117.57.6:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:38.745321262UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>946630</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:00.704189965UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>946627</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-21T07:25:50.659840630UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>946630</td><td>929881</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:02.969315887UTC</td></tr><tr><td>65.108.81.145:26657</td><td>lava-testnet-2</td><td>nodeYarNik 🔴</td><td>946628</td><td>934501</td><td>False</td><td>off</td><td>27252287</td><td>2024-03-21T07:26:34.525770334UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>946632</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:55.780789612UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>946627</td><td>945101</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:25:57.748021472UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>946631</td><td>946441</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T07:27:41.703372692UTC</td></tr></table>
