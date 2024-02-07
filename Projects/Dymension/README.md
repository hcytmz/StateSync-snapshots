<h1 align="center"> 🔥Dymension🔥</h1>

<h1 align="center"> MAINNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

# StateSync Dymension Mainnet
```python
SNAP_RPC=https://dym.rpc.m.stavr.tech:443
peers="e0d84deab2d0fd85f447c5c417fecbbdba584be0@dymension-m.peer.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dymension/config/config.toml
dymd tendermint unsafe-reset-all --home /root/.dymension
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot Mainnet - updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L https://dymension-m.snapshot.stavr.tech/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```


<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension/Testnet)
=

# StateSync Dymension Testnet
```python
SNAP_RPC=https://dym.rpc.t.stavr.tech:443
peers="263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dymension/config/config.toml
dymd tendermint unsafe-reset-all --home /root/.dymension
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot Testnet - updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER-M🔥:     https://explorer.stavr.tech/Dymension-Mainnet/        `Indexer "ON"` \
🔥EXPLORER-T🔥:     https://explorer.stavr.tech/Dymension-testnet/        `Indexer "ON"` \
🔥API-M🔥:          https://dymension.api.m.stavr.tech \
🔥API-T🔥:          https://dymension.api.t.stavr.tech \
🔥RPC-M🔥:          https://dym.rpc.m.stavr.tech:443                  `Snapshot-interval = 1000` \
🔥RPC-T🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC-M🔥:         http://dymension.grpc.m.stavr.tech:7119 \
🔥gRPC-T🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer-M🔥:         `e0d84deab2d0fd85f447c5c417fecbbdba584be0@dymension-m.peer.stavr.tech:17086` \
🔥peer-T🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis-T🔥:     ```wget wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook-M🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Addrbook-T🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/addrbook.json"``` \
🔥Auto_install script-M🔥: ```wget -O dymm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dymm && chmod +x dymm && ./dymm``` \
🔥Auto_install script-T🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/dym && chmod +x dym && ./dym```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dymension/Decentralization)🔥
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

[raw json](https://rpc-check.dymt.stavr.tech/dymt/rpc-dymt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>18206</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:38.106171033UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:40.785241940UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>18207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:41.569482499UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>18207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:41.950936036UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:42.311032531UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>18207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:43.080256789UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18208</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:47.439435655UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>18208</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:50.649872708UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>18209</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:53.024510000UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18209</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:57.444671140UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18212</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:12.080409165UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18212</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:12.969681688UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>18212</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:13.326779478UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18213</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:15.805117653UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18213</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:16.767043593UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>18214</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:21.292810541UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>18214</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:24.277082255UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18214</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:24.664138035UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>18214</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:24.953637376UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>18215</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:26.074085252UTC</td></tr><tr><td>144.91.68.181:26657</td><td>dymension_1100-1</td><td>vmi1526870.contaboserver.net 🟢</td><td>18215</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:26.359574563UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>18215</td><td>1</td><td>False</td><td>off</td><td>505643</td><td>2024-02-07T20:25:28.789841754UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18215</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:29.756055995UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18216</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:36.508585700UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>18217</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:43.083355133UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>18219</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:48.099979081UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18219</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:50.619519560UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18219</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:51.030336488UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18220</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:53.423954041UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>18220</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:55.809715482UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>18221</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-07T20:26:00.245665341UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>18221</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:04.575945361UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18221</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:04.842026845UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18222</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:07.168352913UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18222</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:09.548587906UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18223</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:11.950332394UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18224</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:20.633412352UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18226</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:27.207081942UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18226</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:29.595018190UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>18227</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:34.130650110UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18227</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:34.991526663UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18228</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:39.458745404UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18228</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:42.291540000UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>18228</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:44.688287418UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18229</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:45.761624165UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>18229</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-07T20:26:46.298703679UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18229</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:26:46.699835601UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>18231</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:01.538493524UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>18237</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:32.747889545UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18238</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:37.209700896UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18238</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:39.622999775UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18238</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:40.256511334UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18238</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:42.687883014UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18239</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:43.173549491UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>18240</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:49.586484930UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18240</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:52.054491959UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>18241</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:56.530448705UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18241</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:56.876758827UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>18242</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:27:57.489090898UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>18207</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:24:41.122758671UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>18217</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T20:25:43.447013825UTC</td></tr></table>
