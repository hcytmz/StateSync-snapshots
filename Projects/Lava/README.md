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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.25.109:56657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>980175</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:39.043181977UTC</td></tr><tr><td>158.220.104.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:47.646424382UTC</td></tr><tr><td>161.97.71.152:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:08.456177173UTC</td></tr><tr><td>65.108.206.118:60957</td><td>lava-testnet-2</td><td>UTSA_guide 🔴</td><td>980177</td><td>340778</td><td>False</td><td>on</td><td>10084463</td><td>2024-03-28T11:43:12.217326430UTC</td></tr><tr><td>23.88.70.109:14657</td><td>lava-testnet-2</td><td>Merna 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:12.689355279UTC</td></tr><tr><td>65.21.224.11:26757</td><td>lava-testnet-2</td><td>mynode 🔴</td><td>980178</td><td>340778</td><td>False</td><td>off</td><td>1201009891</td><td>2024-03-28T11:43:21.623177881UTC</td></tr><tr><td>185.196.20.78:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>881586</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:21.930295576UTC</td></tr><tr><td>65.109.25.104:26557</td><td>lava-testnet-2</td><td>5ElementsNodes 🔴</td><td>980181</td><td>340778</td><td>False</td><td>on</td><td>11976722</td><td>2024-03-28T11:44:08.748878031UTC</td></tr><tr><td>65.21.239.60:11657</td><td>lava-testnet-2</td><td>Sergio 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:21.299163103UTC</td></tr><tr><td>89.116.30.32:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:23.640834450UTC</td></tr><tr><td>167.86.85.35:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926699</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:48.968191442UTC</td></tr><tr><td>164.68.110.168:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>926515</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:51.802874607UTC</td></tr><tr><td>161.97.83.43:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>714113</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:59.030204311UTC</td></tr><tr><td>194.34.232.222:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>977343</td><td>340778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:45:04.280133411UTC</td></tr><tr><td>135.181.58.28:23257</td><td>lava-testnet-2</td><td>Validatrium-provider 🟢</td><td>396595</td><td>392778</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:20.977217418UTC</td></tr><tr><td>157.90.128.99:14557</td><td>lava-testnet-2</td><td>Bablovcoin 🔴</td><td>980181</td><td>452778</td><td>False</td><td>on</td><td>15969745</td><td>2024-03-28T11:44:11.528851105UTC</td></tr><tr><td>23.88.74.54:11657</td><td>lava-testnet-2</td><td>Donald 🟢</td><td>714113</td><td>556501</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:12.458110777UTC</td></tr><tr><td>168.119.5.125:14457</td><td>lava-testnet-2</td><td>AlexZ 🔴</td><td>980176</td><td>714061</td><td>False</td><td>on</td><td>12712888</td><td>2024-03-28T11:42:50.517335269UTC</td></tr><tr><td>65.108.75.107:23657</td><td>lava-testnet-2</td><td>node 🟢</td><td>980176</td><td>743001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:54.688924630UTC</td></tr><tr><td>138.201.227.119:14557</td><td>lava-testnet-2</td><td>Monika 🔴</td><td>980183</td><td>751501</td><td>False</td><td>on</td><td>21281037</td><td>2024-03-28T11:44:40.918182738UTC</td></tr><tr><td>216.219.86.126:14457</td><td>lava-testnet-2</td><td>Redbooker 🔴</td><td>980183</td><td>751501</td><td>False</td><td>on</td><td>10611836</td><td>2024-03-28T11:44:48.702872166UTC</td></tr><tr><td>148.251.88.145:10357</td><td>lava-testnet-2</td><td>Palamar 🔴</td><td>980184</td><td>751501</td><td>False</td><td>on</td><td>10159218</td><td>2024-03-28T11:44:56.717515589UTC</td></tr><tr><td>65.109.85.52:46657</td><td>lava-testnet-2</td><td>Pathrocknework 🔴</td><td>980176</td><td>761001</td><td>False</td><td>off</td><td>9093821</td><td>2024-03-28T11:42:57.084280208UTC</td></tr><tr><td>65.109.97.33:26657</td><td>lava-testnet-2</td><td>digital-am 🟢</td><td>845700</td><td>805501</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:47.929042674UTC</td></tr><tr><td>146.148.39.246:26657</td><td>lava-testnet-2</td><td>GoldGlimmer 🟢</td><td>966391</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:44.751866877UTC</td></tr><tr><td>144.76.103.143:14557</td><td>lava-testnet-2</td><td>Monika 🟢</td><td>980176</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:54.390274954UTC</td></tr><tr><td>213.239.194.132:14457</td><td>lava-testnet-2</td><td>node 🔴</td><td>980177</td><td>833001</td><td>False</td><td>on</td><td>20047593</td><td>2024-03-28T11:43:02.097397885UTC</td></tr><tr><td>5.189.147.111:26657</td><td>lava-testnet-2</td><td>lamaj 🟢</td><td>978060</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:15.028281564UTC</td></tr><tr><td>173.212.249.180:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>980168</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:16.582674242UTC</td></tr><tr><td>35.232.218.224:26657</td><td>lava-testnet-2</td><td>LuxLeather 🟢</td><td>966322</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:19.278993425UTC</td></tr><tr><td>38.242.233.70:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>952305</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:31.147865008UTC</td></tr><tr><td>109.199.112.157:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>980178</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:38.799739408UTC</td></tr><tr><td>15.165.182.226:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>977360</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:57.609832697UTC</td></tr><tr><td>51.75.163.241:26657</td><td>lava-testnet-2</td><td>test 🟢</td><td>845700</td><td>833001</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T11:44:09.022460101UTC</td></tr><tr><td>84.247.164.87:14457</td><td>lava-testnet-2</td><td>PARZIVAL 🟢</td><td>956967</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:41.639355358UTC</td></tr><tr><td>37.60.236.238:14457</td><td>lava-testnet-2</td><td>ZLKCyber 🟢</td><td>980183</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:51.557013328UTC</td></tr><tr><td>109.199.97.128:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>979757</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:54.163756846UTC</td></tr><tr><td>109.199.100.238:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>980171</td><td>833001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:56.504195054UTC</td></tr><tr><td>65.109.24.78:17657</td><td>lava-testnet-2</td><td>NodeCtrl 🔴</td><td>980175</td><td>848701</td><td>False</td><td>on</td><td>6025239</td><td>2024-03-28T11:42:41.374897880UTC</td></tr><tr><td>95.217.148.179:35657</td><td>lava-testnet-2</td><td>ksalab 🔴</td><td>980176</td><td>862501</td><td>False</td><td>on</td><td>23408473</td><td>2024-03-28T11:42:47.087084534UTC</td></tr><tr><td>93.159.130.38:28857</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>980181</td><td>862881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:23.966758072UTC</td></tr><tr><td>109.123.247.78:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:48.237455303UTC</td></tr><tr><td>89.117.51.142:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:38.507198556UTC</td></tr><tr><td>173.212.193.103:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>876307</td><td>875881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:49.926123209UTC</td></tr><tr><td>65.109.30.110:11751</td><td>lava-testnet-2</td><td>SerGo 🟢</td><td>980176</td><td>880175</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T11:42:47.380355903UTC</td></tr><tr><td>154.38.167.188:26657</td><td>lava-testnet-2</td><td>wildweststaking 🟢</td><td>979440</td><td>924001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:31.872933741UTC</td></tr><tr><td>5.39.73.22:26657</td><td>lava-testnet-2</td><td>node 🔴</td><td>980175</td><td>926501</td><td>False</td><td>on</td><td>1307699</td><td>2024-03-28T11:42:36.397033300UTC</td></tr><tr><td>188.112.134.197:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>980172</td><td>933881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:12.239584207UTC</td></tr><tr><td>20.67.241.1:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>980182</td><td>933881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:41.269246792UTC</td></tr><tr><td>148.251.9.12:26657</td><td>lava-testnet-2</td><td>guinsous 🟢</td><td>980182</td><td>940801</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:28.421170646UTC</td></tr><tr><td>65.108.227.112:13657</td><td>lava-testnet-2</td><td>[NODERS]TEAM 🔴</td><td>980176</td><td>955881</td><td>False</td><td>on</td><td>9950755</td><td>2024-03-28T11:42:52.917837309UTC</td></tr><tr><td>91.207.54.126:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>972013</td><td>966001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:36.675894170UTC</td></tr><tr><td>23.88.65.15:26657</td><td>lava-testnet-2</td><td>mynode 🟢</td><td>980177</td><td>967881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:36.183549024UTC</td></tr><tr><td>176.9.66.48:14557</td><td>lava-testnet-2</td><td>Mrs_ml 🔴</td><td>980178</td><td>970881</td><td>False</td><td>on</td><td>20286032</td><td>2024-03-28T11:43:24.457058039UTC</td></tr><tr><td>194.163.174.231:26687</td><td>lava-testnet-2</td><td>AviaDoc_by_AviaOne 🟢</td><td>980167</td><td>972301</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:42:43.717868967UTC</td></tr><tr><td>62.171.191.136:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>978607</td><td>973881</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:59.892956360UTC</td></tr><tr><td>43.134.211.5:26657</td><td>lava-testnet-2</td><td>chainbase 🔴</td><td>975661</td><td>975661</td><td>False</td><td>on</td><td>10415138</td><td>2024-03-28T11:42:54.136328363UTC</td></tr><tr><td>75.119.141.156:26657</td><td>lava-testnet-2</td><td>my-node 🟢</td><td>980177</td><td>976285</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:43:24.258436523UTC</td></tr><tr><td>65.108.230.113:198</td><td>lava-testnet-2</td><td>STAVR-Service 🟢</td><td>980181</td><td>979921</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T11:44:11.835877137UTC</td></tr></table>
