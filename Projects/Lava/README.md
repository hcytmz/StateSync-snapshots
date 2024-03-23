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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>954435</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:37.555773900UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:46.148705996UTC</td></tr><tr><td>195.201.164.54:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954436</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:54.865475586UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:12.252188199UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>954437</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-23T04:39:16.308183661UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:17.127427584UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>954437</td><td>340778</td><td>False</td><td>off</td><td>1200907387</td><td>2024-03-23T04:39:27.064594803UTC</td></tr><tr><td>109.199.117.254:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954438</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:38.140350022UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>954440</td><td>340778</td><td>False</td><td>on</td><td>11976722</td><td>2024-03-23T04:40:13.941077711UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:28.187675844UTC</td></tr><tr><td>89.163.153.22:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954440</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:30.461958838UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:30.758791693UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:53.918986795UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:41:05.028483173UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954442</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:41:10.289485668UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:27.888725177UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>954440</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-23T04:40:16.834945649UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:16.841366874UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>954436</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-23T04:38:48.708506754UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>954436</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:55.178524799UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>954441</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-23T04:40:50.985210029UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>954442</td><td>751501</td><td>False</td><td>on</td><td>10104218</td><td>2024-03-23T04:41:02.738229834UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>954436</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-23T04:38:59.563885669UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>954437</td><td>762001</td><td>False</td><td>on</td><td>20286032</td><td>2024-03-23T04:39:29.364073824UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>954436</td><td>764041</td><td>False</td><td>on</td><td>9950755</td><td>2024-03-23T04:38:51.167126428UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:46.459421312UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>954435</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:42.928576721UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>954436</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:54.618496012UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>954436</td><td>833001</td><td>False</td><td>on</td><td>20047592</td><td>2024-03-23T04:39:05.882251180UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>954437</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:19.426183877UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>954437</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:21.745395379UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954437</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:21.999583335UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>954437</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:24.714887199UTC</td></tr><tr><td>88.198.230.219:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>954440</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:13.638312837UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-23T04:40:14.223562754UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>954441</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:46.084745969UTC</td></tr><tr><td>173.212.192.130:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>904767</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:48.354742060UTC</td></tr><tr><td>161.97.76.144:26657</td><td>lava-testnet-2</td><td>f52y0u 🟢</td><td>954428</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:51.303583846UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>954441</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:53.653539073UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954442</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:41:01.758395956UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>954435</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-23T04:38:39.883940665UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>954436</td><td>854435</td><td>False</td><td>off</td><td>0</td><td>2024-03-23T04:38:45.865238061UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>927794</td><td>859261</td><td>False</td><td>on</td><td>10520341</td><td>2024-03-23T04:38:52.350186752UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>954436</td><td>862501</td><td>False</td><td>on</td><td>23408472</td><td>2024-03-23T04:38:45.554860799UTC</td></tr><tr><td>84.46.255.68:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:12.556864556UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:43.491827863UTC</td></tr><tr><td>173.212.193.212:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:45.804835840UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>954438</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:38.878601675UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>954435</td><td>926501</td><td>False</td><td>on</td><td>1247699</td><td>2024-03-23T04:38:35.223556877UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>954438</td><td>929881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:39:41.150447852UTC</td></tr><tr><td>20.67.241.1:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>954441</td><td>933881</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:45.734282550UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>954441</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:33.174650559UTC</td></tr><tr><td>65.108.81.145:26657</td><td>lava-testnet-2</td><td>nodeYarNik 🔴</td><td>954437</td><td>948001</td><td>False</td><td>off</td><td>27252287</td><td>2024-03-23T04:39:16.621594203UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>954435</td><td>953401</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:38:42.218374690UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>954440</td><td>954301</td><td>False</td><td>on</td><td>0</td><td>2024-03-23T04:40:17.142837256UTC</td></tr></table>
