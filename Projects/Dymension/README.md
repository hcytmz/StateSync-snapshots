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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>2240</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:08.782936781UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2240</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:11.881898731UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>2240</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:12.620349911UTC</td></tr><tr><td>5.78.103.84:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2241</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:13.547625616UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>2241</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:14.202733741UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2243</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:24.774069204UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2244</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:35.366047346UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2244</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:36.301089738UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>2245</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:36.671545883UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2245</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:39.059603800UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2245</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:40.073034530UTC</td></tr><tr><td>45.76.86.41:26657</td><td>dymension_1100-1</td><td>KudasaiJP 🔴</td><td>2245</td><td>1</td><td>False</td><td>on</td><td>53637</td><td>2024-02-06T17:27:42.385938138UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>2246</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:44.858931999UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2246</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:47.283719175UTC</td></tr><tr><td>91.107.208.199:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2246</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:47.561823952UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>2246</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:47.878068408UTC</td></tr><tr><td>144.91.68.181:26657</td><td>dymension_1100-1</td><td>vmi1526870.contaboserver.net 🟢</td><td>2246</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:48.223374281UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>2247</td><td>1</td><td>False</td><td>off</td><td>76988</td><td>2024-02-06T17:27:50.635506446UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2247</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:51.567481170UTC</td></tr><tr><td>167.235.9.223:61657</td><td>dymension_1100-1</td><td>F5Nodes 🟢</td><td>1</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-06T17:27:53.910272758UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2248</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:54.298773100UTC</td></tr><tr><td>49.13.63.87:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2248</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:54.590440940UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>2248</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:58.991039323UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>2249</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:03.555391382UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2249</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:05.980141877UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2250</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:06.390498103UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2250</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:06.753889371UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>2250</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:09.110735931UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>2250</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:11.437649502UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>2251</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:13.755427181UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2251</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:16.174083051UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2252</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:18.528468530UTC</td></tr><tr><td>5.161.103.111:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2252</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:21.211762204UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2252</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:21.472650718UTC</td></tr><tr><td>5.78.84.136:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2252</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:22.506752406UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2253</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:24.905841987UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2254</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:33.492639781UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2255</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:40.512476353UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>2255</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:40.837087262UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2255</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:41.680729719UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2256</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:46.192376684UTC</td></tr><tr><td>5.78.114.208:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2256</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:47.188974036UTC</td></tr><tr><td>5.78.68.191:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2257</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:50.239423933UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2257</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:50.944690465UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>2257</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:53.275013705UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2258</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:54.239253901UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2258</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:54.687981876UTC</td></tr><tr><td>49.13.133.97:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2259</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:03.260552789UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>2259</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:03.584805075UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2260</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:08.141220394UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>2263</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:33.129974000UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2265</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:35.550812350UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2265</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:40.086614533UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2265</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:40.745858588UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2266</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:43.244607490UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2266</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:43.613940024UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>2266</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:46.007546108UTC</td></tr><tr><td>5.78.95.189:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2266</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:47.026897168UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2266</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:47.300121728UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>2267</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:53.850857778UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2268</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:54.332911261UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2268</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:55.020146857UTC</td></tr><tr><td>5.75.239.133:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>2268</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:29:55.304169335UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>2240</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:27:12.246771834UTC</td></tr><tr><td>37.27.59.176:14657</td><td>dymension_1100-1</td><td>luciolaKami 🟢</td><td>2255</td><td>383</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T17:28:40.099319363UTC</td></tr></table>
