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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:21.907254310UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:45.809988846UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:52.755214870UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>930809</td><td>340778</td><td>False</td><td>off</td><td>1200856875</td><td>2024-03-16T20:38:02.059371249UTC</td></tr><tr><td>185.196.20.78:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>881586</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:02.382510634UTC</td></tr><tr><td>109.199.117.254:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>930810</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:13.393782152UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>930810</td><td>340778</td><td>False</td><td>on</td><td>11976721</td><td>2024-03-16T20:39:00.982983935UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:10.823450948UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>930810</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:13.133600253UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:13.482351134UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:33.551752641UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:44.302270978UTC</td></tr><tr><td>167.86.82.9:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926971</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:46.589199186UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>930811</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:46.893938649UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>930810</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-16T20:39:04.096731222UTC</td></tr><tr><td>78.46.103.246:60557</td><td>lava-testnet-2</td><td>F5Nodes 🔴</td><td>930810</td><td>452881</td><td>False</td><td>off</td><td>14846389</td><td>2024-03-16T20:39:01.513860385UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:52.517954865UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>930808</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-16T20:37:24.038943836UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>930808</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:28.768589424UTC</td></tr><tr><td>152.32.211.182:26657</td><td>lava-testnet-2</td><td>my-node 🔴</td><td>930808</td><td>751501</td><td>False</td><td>on</td><td>1082704637</td><td>2024-03-16T20:37:23.134258721UTC</td></tr><tr><td>138.201.227.119:14557</td><td>lava-testnet-2</td><td>Monika 🔴</td><td>930810</td><td>751501</td><td>False</td><td>on</td><td>22281036</td><td>2024-03-16T20:39:24.639729544UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>930810</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-16T20:39:29.607524535UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>930811</td><td>751501</td><td>False</td><td>on</td><td>10104217</td><td>2024-03-16T20:39:41.308131252UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>930809</td><td>762001</td><td>False</td><td>on</td><td>21286031</td><td>2024-03-16T20:38:04.638873948UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>930808</td><td>764041</td><td>False</td><td>on</td><td>9950754</td><td>2024-03-16T20:37:26.463867293UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:23.436205401UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>930808</td><td>830808</td><td>False</td><td>off</td><td>0</td><td>2024-03-16T20:37:19.600837376UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>927794</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:16.882997866UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>albinos 🔴</td><td>930809</td><td>833001</td><td>False</td><td>on</td><td>20047592</td><td>2024-03-16T20:37:39.447114682UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>930809</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:53.036578982UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>930809</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:55.365002049UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>927794</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:59.702313586UTC</td></tr><tr><td>109.199.112.157:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>930810</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:22.937998940UTC</td></tr><tr><td>94.72.120.27:26657</td><td>lava-testnet-2</td><td>RAVENODE 🟢</td><td>930810</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:30.445695952UTC</td></tr><tr><td>62.171.191.136:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>930810</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:51.719622606UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-16T20:39:01.278173372UTC</td></tr><tr><td>173.212.192.130:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>904767</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:26.986655022UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>930810</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:31.952244944UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>930811</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:37.935298105UTC</td></tr><tr><td>193.203.162.124:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>927794</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:42.006640585UTC</td></tr><tr><td>135.148.148.240:26657</td><td>lava-testnet-2</td><td>ProtofireDAO 🟢</td><td>930810</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:47.519520623UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>930808</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-16T20:37:13.765827296UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>927794</td><td>859261</td><td>False</td><td>on</td><td>10520341</td><td>2024-03-16T20:37:27.660390938UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>930808</td><td>862501</td><td>False</td><td>on</td><td>23408471</td><td>2024-03-16T20:37:19.236413776UTC</td></tr><tr><td>93.159.130.38:28857</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>930810</td><td>862881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:13.823887700UTC</td></tr><tr><td>109.123.247.78:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:23.824159084UTC</td></tr><tr><td>84.46.255.1:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:28.262280451UTC</td></tr><tr><td>84.46.255.68:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:46.110756109UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:20.571437036UTC</td></tr><tr><td>173.212.193.103:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:41.194039389UTC</td></tr><tr><td>89.117.57.6:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:01.817344891UTC</td></tr><tr><td>135.181.238.30:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>927794</td><td>911641</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:56.997237421UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>927794</td><td>911641</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:39:16.220315229UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>930810</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:38:14.119049723UTC</td></tr><tr><td>65.108.81.145:26657</td><td>lava-testnet-2</td><td>nodeYarNik 🔴</td><td>930809</td><td>926001</td><td>False</td><td>off</td><td>27252287</td><td>2024-03-16T20:37:50.255307985UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>930808</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-16T20:37:09.364626590UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>930808</td><td>928681</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T20:37:16.186034913UTC</td></tr></table>
