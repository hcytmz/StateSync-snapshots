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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>5930</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:34.125209579UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5930</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:36.836258299UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>5930</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:37.623825363UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>5930</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:37.959692227UTC</td></tr><tr><td>5.78.103.84:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5930</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:38.908540328UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5931</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:39.269198432UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>5931</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:39.948213536UTC</td></tr><tr><td>95.216.142.40:26657</td><td>dymension_1100-1</td><td>inklbot 🟢</td><td>5931</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:44.477327796UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>5932</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:47.449729924UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>5932</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:47.757169611UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5933</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:52.118980503UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5934</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:03.247205945UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>5934</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:03.628220630UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5935</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:08.247988300UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5935</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:09.210768619UTC</td></tr><tr><td>45.76.86.41:26657</td><td>dymension_1100-1</td><td>KudasaiJP 🔴</td><td>5936</td><td>1</td><td>False</td><td>on</td><td>85200</td><td>2024-02-06T23:43:11.531019388UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>5936</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:13.988245874UTC</td></tr><tr><td>5.78.111.114:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:17.011511302UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:17.368308022UTC</td></tr><tr><td>91.107.208.199:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:17.659229101UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>5937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:17.916486884UTC</td></tr><tr><td>144.91.68.181:26657</td><td>dymension_1100-1</td><td>vmi1526870.contaboserver.net 🟢</td><td>5937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:18.202279446UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>5937</td><td>1</td><td>False</td><td>off</td><td>290216</td><td>2024-02-06T23:43:20.714775370UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:21.625338079UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5938</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:26.144354271UTC</td></tr><tr><td>49.13.63.87:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5938</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:26.439216700UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>5939</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:30.897091955UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>5940</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:35.543380550UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5940</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:37.952615840UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5940</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:38.397484672UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5940</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:40.857498931UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>5940</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:41.142372920UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>5941</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:47.681792528UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>5942</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:50.050084624UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5942</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:52.355744672UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5943</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:54.733654722UTC</td></tr><tr><td>5.161.103.111:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5943</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:57.563436853UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5943</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:57.847728929UTC</td></tr><tr><td>5.78.84.136:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5943</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:43:58.768574132UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5944</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:01.191367495UTC</td></tr><tr><td>5.78.98.90:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5944</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:06.261654095UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5945</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:08.717498610UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5946</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:13.201910989UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5946</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:16.079209303UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>5947</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:20.514816167UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5947</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:21.488039154UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5948</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:26.003896378UTC</td></tr><tr><td>5.78.114.208:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5948</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:26.927877687UTC</td></tr><tr><td>5.78.68.191:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5948</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:29.974532410UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5948</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:30.609527652UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>5949</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:33.017559970UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5949</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:33.964724180UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>5949</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-06T23:44:34.390880196UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5949</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:34.785709090UTC</td></tr><tr><td>49.13.133.97:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5950</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:43.262597142UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>5950</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:43.626937092UTC</td></tr><tr><td>5.78.114.153:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5951</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:48.695901781UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5952</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:51.175285158UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>5955</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:14.241578227UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5956</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:16.658131765UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5957</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:23.220052441UTC</td></tr><tr><td>5.78.94.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5957</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:24.172324210UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5957</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:24.807592949UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5958</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:27.219105280UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5958</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:27.594429744UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>5958</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:31.952810055UTC</td></tr><tr><td>5.78.95.189:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5958</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:32.903246652UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5959</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:33.206375335UTC</td></tr><tr><td>5.78.81.63:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5959</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:38.236974258UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>5960</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:40.666048786UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5960</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:41.086552579UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5960</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:41.738836101UTC</td></tr><tr><td>5.75.239.133:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>5960</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:45:42.015246863UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>5930</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:42:37.251210418UTC</td></tr><tr><td>37.27.59.176:14657</td><td>dymension_1100-1</td><td>luciolaKami 🟢</td><td>5946</td><td>383</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T23:44:15.719589404UTC</td></tr></table>
