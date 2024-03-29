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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>984486</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:13.232238581UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:24.474721621UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:42.537127510UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>984488</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-29T08:10:46.303772137UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:46.775699731UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>984489</td><td>340778</td><td>False</td><td>off</td><td>1201009892</td><td>2024-03-29T08:10:52.901036685UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>984491</td><td>340778</td><td>False</td><td>on</td><td>11976722</td><td>2024-03-29T08:11:38.338973810UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:49.962269082UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:52.549672004UTC</td></tr><tr><td>173.212.208.191:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>912954</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:08.154215775UTC</td></tr><tr><td>167.86.85.35:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926699</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:13.131473571UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:16.614947793UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:23.552703979UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>980461</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:27.928528776UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>984492</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-29T08:11:41.161945481UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:46.556203734UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>984487</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-29T08:10:27.066463618UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>984487</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:29.144919044UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>984494</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-29T08:12:13.703368577UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>984494</td><td>751501</td><td>False</td><td>on</td><td>10159218</td><td>2024-03-29T08:12:21.267177956UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>984487</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-29T08:10:31.503148851UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:24.781960443UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>966391</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:19.500700476UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>984488</td><td>833001</td><td>False</td><td>on</td><td>20047593</td><td>2024-03-29T08:10:36.152217658UTC</td></tr><tr><td>57.128.95.99:26657</td><td>lava-testnet-2</td><td>donkamote 🟢</td><td>984488</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:47.025846662UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>980766</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:49.397807524UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>984488</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:49.875531807UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>966322</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:50.547162414UTC</td></tr><tr><td>217.160.220.223:14557</td><td>lava-testnet-2</td><td>BSAL 🟢</td><td>984489</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:05.516891409UTC</td></tr><tr><td>109.199.112.157:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>984489</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:05.823301861UTC</td></tr><tr><td>88.198.230.219:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>984491</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:38.020510072UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-29T08:11:38.608958679UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>956967</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:08.466715731UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>984493</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:16.332828536UTC</td></tr><tr><td>109.199.97.128:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>983820</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:12:19.023513930UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>984487</td><td>862501</td><td>False</td><td>on</td><td>23408473</td><td>2024-03-29T08:10:21.837278672UTC</td></tr><tr><td>93.159.130.38:28857</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>984492</td><td>862881</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:52.814183829UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:05.237991195UTC</td></tr><tr><td>173.212.193.103:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:21.066233721UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>984487</td><td>884487</td><td>False</td><td>off</td><td>0</td><td>2024-03-29T08:10:22.138728350UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>984300</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:55.216406057UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>984487</td><td>955881</td><td>False</td><td>on</td><td>9950755</td><td>2024-03-29T08:10:27.412122144UTC</td></tr><tr><td>91.207.54.126:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>973024</td><td>966001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:10.858182233UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>984489</td><td>967881</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:02.920896190UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>984489</td><td>970881</td><td>False</td><td>on</td><td>20286032</td><td>2024-03-29T08:10:55.457172759UTC</td></tr><tr><td>75.119.141.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>984489</td><td>976285</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:55.224180003UTC</td></tr><tr><td>65.108.66.220:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>984493</td><td>978861</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:57.581736751UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>984486</td><td>980001</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-29T08:10:15.595321745UTC</td></tr><tr><td>85.215.32.123:14557</td><td>lava-testnet-2</td><td>BSE 🟢</td><td>984492</td><td>980173</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:52.261148320UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>984487</td><td>981417</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:10:28.844856704UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>984492</td><td>984181</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T08:11:41.477684089UTC</td></tr></table>
