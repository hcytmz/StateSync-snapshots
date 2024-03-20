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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>941408</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:24.655977507UTC</td></tr><tr><td>109.123.251.165:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941408</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:29.375321726UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:35.039482187UTC</td></tr><tr><td>195.201.164.54:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941409</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:42.675063525UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:02.504664838UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>941410</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-20T02:39:06.831797510UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:09.654629222UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>941410</td><td>340778</td><td>False</td><td>off</td><td>1200856880</td><td>2024-03-20T02:39:19.010429871UTC</td></tr><tr><td>109.199.117.254:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941411</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:30.387990912UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>941413</td><td>340778</td><td>False</td><td>on</td><td>11976721</td><td>2024-03-20T02:40:11.853117333UTC</td></tr><tr><td>109.199.116.90:26657</td><td>lava-testnet-2</td><td>InkyaNode 🟢</td><td>931947</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:14.768506373UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:22.009906285UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941414</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:24.292691469UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:24.600903322UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:54.535851970UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:41:06.684306125UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941416</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:41:14.529957423UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:21.700360615UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>941413</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-20T02:40:14.982151162UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:09.411400227UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>941408</td><td>714061</td><td>False</td><td>on</td><td>12712887</td><td>2024-03-20T02:38:37.920826386UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>941409</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:42.994782681UTC</td></tr><tr><td>138.201.227.119:14557</td><td>lava-testnet-2</td><td>Monika 🔴</td><td>941415</td><td>751501</td><td>False</td><td>on</td><td>22281036</td><td>2024-03-20T02:40:41.591240548UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>941415</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-20T02:40:48.324979890UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>941416</td><td>751501</td><td>False</td><td>on</td><td>10104217</td><td>2024-03-20T02:41:04.387437083UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>941410</td><td>762001</td><td>False</td><td>on</td><td>21286031</td><td>2024-03-20T02:39:21.306718085UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>941409</td><td>764041</td><td>False</td><td>on</td><td>9950754</td><td>2024-03-20T02:38:40.324362947UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:35.340209249UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>941409</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:42.112273070UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>941409</td><td>833001</td><td>False</td><td>on</td><td>20047592</td><td>2024-03-20T02:38:56.133922610UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>941410</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:11.968739277UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>941410</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:14.446176281UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941410</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:15.968380960UTC</td></tr><tr><td>38.242.233.70:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941411</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:30.082489514UTC</td></tr><tr><td>109.199.112.157:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941411</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:40.143885440UTC</td></tr><tr><td>15.165.182.226:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>941412</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:58.699640520UTC</td></tr><tr><td>62.171.191.136:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941410</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:03.130935364UTC</td></tr><tr><td>88.198.230.219:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>941413</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:11.563431682UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-20T02:40:12.135029074UTC</td></tr><tr><td>161.97.76.144:26657</td><td>lava-testnet-2</td><td>f52y0u 🟢</td><td>941415</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:48.616905023UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>941415</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:50.921075276UTC</td></tr><tr><td>109.199.97.128:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941416</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:41:00.994402910UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>941416</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:41:03.329968571UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>941408</td><td>841408</td><td>False</td><td>off</td><td>0</td><td>2024-03-20T02:38:32.701246279UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>941408</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-20T02:38:27.039705572UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>927794</td><td>859261</td><td>False</td><td>on</td><td>10520341</td><td>2024-03-20T02:38:41.509057198UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>941408</td><td>862501</td><td>False</td><td>on</td><td>23408471</td><td>2024-03-20T02:38:32.382922945UTC</td></tr><tr><td>93.159.130.38:28857</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>941414</td><td>862881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:24.888546311UTC</td></tr><tr><td>109.123.247.78:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:35.644944192UTC</td></tr><tr><td>84.46.255.1:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:42.436254713UTC</td></tr><tr><td>84.46.255.68:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:02.801067990UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:37.764221683UTC</td></tr><tr><td>89.117.57.6:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:40:12.474665689UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>941411</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:31.156796720UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>941407</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-20T02:38:22.309762698UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>941411</td><td>929881</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:39:35.466459809UTC</td></tr><tr><td>65.108.81.145:26657</td><td>lava-testnet-2</td><td>nodeYarNik 🔴</td><td>941410</td><td>934501</td><td>False</td><td>off</td><td>27252287</td><td>2024-03-20T02:39:07.150873443UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>941408</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-20T02:38:29.676388113UTC</td></tr></table>
