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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>960388</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:03.333103676UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:11.602319428UTC</td></tr><tr><td>195.201.164.54:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960389</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:20.256197462UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:35.914612883UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:40.394527355UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>960391</td><td>340778</td><td>False</td><td>off</td><td>1200908380</td><td>2024-03-24T13:29:54.486297883UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>960394</td><td>340778</td><td>False</td><td>on</td><td>11976722</td><td>2024-03-24T13:30:43.740135078UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:56.018705953UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960395</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:58.292296542UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:58.574984977UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:22.223150749UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:31.635301182UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960397</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:34.928348083UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:55.694359608UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>960394</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-24T13:30:46.625401179UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:40.139048328UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>960388</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-24T13:29:14.146397232UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>960389</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:20.582133454UTC</td></tr><tr><td>138.201.227.119:14557</td><td>lava-testnet-2</td><td>Monika 🔴</td><td>960396</td><td>751501</td><td>False</td><td>on</td><td>21281037</td><td>2024-03-24T13:31:13.905852302UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>960396</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-24T13:31:19.211050220UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>960397</td><td>751501</td><td>False</td><td>on</td><td>10104218</td><td>2024-03-24T13:31:29.333424088UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>960389</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-24T13:29:24.973975825UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>960391</td><td>762001</td><td>False</td><td>on</td><td>20286032</td><td>2024-03-24T13:29:56.729420352UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:11.899902181UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>960388</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:08.718205469UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>960389</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:20.043373168UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>960389</td><td>833001</td><td>False</td><td>on</td><td>20047592</td><td>2024-03-24T13:29:29.552767382UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>960390</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:42.686231093UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>960389</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:45.005567728UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960391</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:49.401324757UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>960391</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:52.122368917UTC</td></tr><tr><td>62.171.191.136:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>959820</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:34.658931329UTC</td></tr><tr><td>88.198.230.219:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>960394</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:43.400385042UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-24T13:30:44.060850750UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>956967</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:14.527251785UTC</td></tr><tr><td>161.97.76.144:26657</td><td>lava-testnet-2</td><td>f52y0u 🟢</td><td>960379</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:19.630861246UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>960396</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:21.981360665UTC</td></tr><tr><td>109.199.97.128:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960397</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:26.668800987UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960397</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:29.040602751UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>960388</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-24T13:29:05.697190259UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>927794</td><td>859261</td><td>False</td><td>on</td><td>10520341</td><td>2024-03-24T13:29:17.764954363UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>960388</td><td>860388</td><td>False</td><td>off</td><td>0</td><td>2024-03-24T13:29:11.348779874UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>960388</td><td>862501</td><td>False</td><td>on</td><td>23408472</td><td>2024-03-24T13:29:11.058387912UTC</td></tr><tr><td>93.159.130.38:28857</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>960395</td><td>862881</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:58.895116942UTC</td></tr><tr><td>84.46.255.68:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:36.202344805UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:10.620827569UTC</td></tr><tr><td>173.212.193.212:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:12.935630318UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>960392</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:05.971828920UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>960388</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-24T13:29:00.964702278UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>960392</td><td>929881</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:08.260053279UTC</td></tr><tr><td>20.67.241.1:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>960396</td><td>933881</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:14.214476728UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>960395</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:31:03.300419720UTC</td></tr><tr><td>65.108.81.145:26657</td><td>lava-testnet-2</td><td>nodeYarNik 🔴</td><td>960390</td><td>948001</td><td>False</td><td>off</td><td>27252288</td><td>2024-03-24T13:29:39.911739621UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>960389</td><td>955881</td><td>False</td><td>on</td><td>9950755</td><td>2024-03-24T13:29:16.558695348UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>960388</td><td>957701</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:29:08.044824973UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>960394</td><td>959001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T13:30:46.932877603UTC</td></tr></table>
