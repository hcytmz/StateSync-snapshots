[🔥OUR VALIDATOR🔥](https://restake.app/dymension/dymvaloper1amxp0k0hg4edrxg85v07t9ka2tfuhamhldgf8e)
=

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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>33901</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:19.505810457UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:24.245755798UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>33902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:24.971208838UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>33902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:25.341923568UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:25.742004356UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>33902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:26.371062503UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33903</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:30.805238501UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>33903</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:33.788191478UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>33904</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:36.148723411UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33905</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:40.605470797UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33907</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:53.261171631UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33907</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:54.113733392UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>33907</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:54.460012042UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33908</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:56.911540709UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33908</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:57.878417290UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>33909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:02.458899666UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>33909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:02.969102216UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>33909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:03.920673484UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:04.272491269UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>33909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:04.528463782UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>33909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:05.668232858UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>33910</td><td>1</td><td>False</td><td>off</td><td>583189</td><td>2024-02-08T21:19:08.043780479UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33910</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:09.015421274UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33911</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:15.736487021UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>33913</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:26.855401212UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33913</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:29.337494078UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33913</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:29.714518864UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33914</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:32.140203016UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>33914</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:34.490325100UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>33915</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T21:19:39.063717331UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>33915</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:41.368252753UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33915</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:43.743605617UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33916</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:46.425313025UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33916</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:48.729192991UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33917</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:53.189557105UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33919</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:03.869240162UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33920</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:08.367147767UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>33921</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:14.856197983UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33921</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:15.740891589UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33922</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:20.285705244UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33922</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:21.344386370UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>33922</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:23.777156319UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33923</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:24.807605836UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>33923</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T21:20:25.244906374UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33923</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:27.751262436UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>33926</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:42.652875121UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33927</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:49.233180948UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>33931</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:12.192428843UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33931</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:16.659289604UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>33930</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:19.096457743UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33933</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:23.630659834UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33933</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:24.263040512UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33933</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:26.682890094UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33933</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:27.140505405UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>33935</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:33.540598366UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33935</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:35.898339939UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>33936</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:40.410298168UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33936</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:40.821938012UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>33936</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:21:41.429848464UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>33902</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:18:24.596450365UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>33912</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:22.274094245UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>33922</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:20:20.650791893UTC</td></tr><tr><td>78.47.67.0:26657</td><td>dymension_1100-1</td><td>bfxd 🟢</td><td>26001</td><td>26001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T21:19:44.023501734UTC</td></tr></table>
