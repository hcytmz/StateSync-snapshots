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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>953662</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:12.246701429UTC</td></tr><tr><td>109.123.251.165:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953662</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:16.979830441UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:23.202503062UTC</td></tr><tr><td>195.201.164.54:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953663</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:31.839716521UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:49.225320558UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>953664</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-23T00:32:53.256084622UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:54.011695904UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>953665</td><td>340778</td><td>False</td><td>off</td><td>1200907386</td><td>2024-03-23T00:33:04.189354157UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>953668</td><td>340778</td><td>False</td><td>on</td><td>11976722</td><td>2024-03-23T00:33:54.527114342UTC</td></tr><tr><td>109.199.116.90:26657</td><td>lava-testnet-2</td><td>InkyaNode 🟢</td><td>931947</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:57.457701895UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:08.786048478UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953669</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:11.067107645UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:11.334568790UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:34.534336114UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:45.744144366UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953671</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:51.031148843UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:08.471427380UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>953668</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-23T00:33:57.689285444UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:53.775927591UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>953663</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-23T00:32:25.817502919UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>953663</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:32.145476571UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>953670</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-23T00:34:31.640708568UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>953671</td><td>751501</td><td>False</td><td>on</td><td>10104218</td><td>2024-03-23T00:34:43.467700355UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>953663</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-23T00:32:36.517823944UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>953665</td><td>762001</td><td>False</td><td>on</td><td>20286032</td><td>2024-03-23T00:33:06.481404292UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>953663</td><td>764041</td><td>False</td><td>on</td><td>9950755</td><td>2024-03-23T00:32:28.199678062UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:23.518867245UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>953662</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:17.944690072UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>953663</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:31.629828379UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>953664</td><td>833001</td><td>False</td><td>on</td><td>20047592</td><td>2024-03-23T00:32:42.874596797UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>953664</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:56.315778537UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>953665</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:58.646776560UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953665</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:01.140007075UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>953665</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:03.862750156UTC</td></tr><tr><td>38.242.233.70:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>952305</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:15.275790902UTC</td></tr><tr><td>15.165.182.226:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>953667</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:41.428626264UTC</td></tr><tr><td>88.198.230.219:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>953668</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:54.187343149UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-23T00:33:54.780530343UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>953670</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:26.688021387UTC</td></tr><tr><td>173.212.192.130:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>904767</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:29.003994835UTC</td></tr><tr><td>161.97.76.144:26657</td><td>lava-testnet-2</td><td>f52y0u 🟢</td><td>953670</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:31.919965177UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>953670</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:34.255076657UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953671</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:42.452401725UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>953662</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-23T00:32:14.589580453UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>953662</td><td>853662</td><td>False</td><td>off</td><td>0</td><td>2024-03-23T00:32:20.859471764UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>927794</td><td>859261</td><td>False</td><td>on</td><td>10520341</td><td>2024-03-23T00:32:29.386635182UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>953662</td><td>862501</td><td>False</td><td>on</td><td>23408472</td><td>2024-03-23T00:32:20.558999340UTC</td></tr><tr><td>84.46.255.68:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:49.519682287UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:20.605054283UTC</td></tr><tr><td>173.212.193.212:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:22.895427425UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>953666</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:16.001965967UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>953662</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-23T00:32:09.907685861UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>953666</td><td>929881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:18.273951935UTC</td></tr><tr><td>20.67.241.1:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>953670</td><td>933881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:26.375759693UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>953669</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:34:13.703734957UTC</td></tr><tr><td>65.108.81.145:26657</td><td>lava-testnet-2</td><td>nodeYarNik 🔴</td><td>953664</td><td>948001</td><td>False</td><td>off</td><td>27252287</td><td>2024-03-23T00:32:53.566258532UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>953668</td><td>953341</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:33:57.993268917UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>953662</td><td>953401</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T00:32:17.282254664UTC</td></tr></table>
