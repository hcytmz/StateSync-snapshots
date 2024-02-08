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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>20826</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:35.909718675UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20827</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:40.796614702UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>20827</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:41.498336870UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>20827</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:41.859477063UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20827</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:42.222233826UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>20827</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:42.941363762UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20828</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:47.386340170UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>20829</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:50.279252953UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>20829</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:52.617756245UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20830</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:56.992652768UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20832</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:09.697540051UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20832</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:10.627262878UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>20832</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:10.982990343UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20832</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:13.454999424UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20833</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:14.397561075UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>20834</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:18.878026338UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>20834</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:21.832713162UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20835</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:22.174241081UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>20835</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:22.445450621UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>20835</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:23.570412706UTC</td></tr><tr><td>144.91.68.181:26657</td><td>dymension_1100-1</td><td>vmi1526870.contaboserver.net 🟢</td><td>20835</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:23.848629025UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>20835</td><td>1</td><td>False</td><td>off</td><td>536185</td><td>2024-02-08T00:34:26.260910743UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20835</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:27.188506118UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20836</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:33.972627028UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>20837</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:40.423813047UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>20838</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:45.400595861UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:47.765585636UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:48.176531711UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:50.634131204UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>20839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:53.060574279UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>20840</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T00:34:57.545064011UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>20842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:01.939842772UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:02.198488033UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:04.564143870UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:06.954556068UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20843</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:09.364363344UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20844</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:18.015747661UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20845</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:24.540549794UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20846</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:27.016281749UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>20846</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:31.431580756UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20846</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:32.415103440UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20847</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:36.904934521UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20848</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:40.265423176UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>20848</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:42.601185736UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20848</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:43.532349414UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>20848</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T00:35:44.001408335UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20849</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:46.399516323UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>20852</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:01.261462615UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>20857</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:32.681589210UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20858</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:37.118572220UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20858</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:39.598779716UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20859</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:40.326269951UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20859</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:42.775383328UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20859</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:43.231123419UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>20860</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:49.643588152UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20861</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:51.981396749UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>20861</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:56.420715573UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20861</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:56.795301667UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>20861</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:36:57.510409318UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>20827</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:33:41.140610182UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>20837</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:34:40.793077884UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>20848</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T00:35:39.342071362UTC</td></tr></table>
