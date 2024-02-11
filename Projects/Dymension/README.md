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

<h4 align="center"> 🔥ARCHIVE NODE🔥    </h4>

API https://dym.api-archive.m.stavr.tech/ \
RPC https://dym.rpc-archive.m.stavr.tech/

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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>70584</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:33.593010206UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70584</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:38.340198584UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>70585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:39.026051895UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>70585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:39.378575620UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:39.755738234UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>70585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:40.490236736UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:42.839187486UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>70586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:45.710446371UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>70586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:48.096955253UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:50.578980200UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70590</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:05.319591267UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70590</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:08.318163762UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>70590</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:08.680119492UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70591</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:11.102892714UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70591</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:12.046419348UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>70592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:16.513954256UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>70592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:16.974190695UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>70592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:17.983866470UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:20.708643187UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>70592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:21.011816907UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>70592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:22.084132966UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>70593</td><td>1</td><td>False</td><td>off</td><td>621809</td><td>2024-02-11T07:26:24.610811470UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:25.562681297UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70594</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:30.358027695UTC</td></tr><tr><td>65.21.229.60:37657</td><td>dymension_1100-1</td><td>r-index-bh 🟢</td><td>70593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:32.725026964UTC</td></tr><tr><td>75.119.139.53:26667</td><td>dymension_1100-1</td><td>AVIAONE_Blockchains_Service 🟢</td><td>70595</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:37.171190922UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70596</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:44.059401098UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70596</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:46.484865627UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>70597</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:49.236759160UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>70598</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-11T07:26:53.739802130UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>70598</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:58.082335969UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70598</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:58.362277176UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70600</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:00.970617541UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70600</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:03.322642945UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70601</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:07.842094516UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70603</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:20.539633240UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70604</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:27.064901473UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70604</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:29.471213672UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>70605</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:33.992631969UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70606</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:38.419969640UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70606</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:39.473324677UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>70606</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:41.908355191UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70606</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:42.866014305UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>70606</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-11T07:27:43.345910813UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70610</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:04.904722012UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>70615</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:27.990684010UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70615</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:30.428884628UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>70615</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:32.866424285UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70616</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:37.402496294UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70616</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:38.122235529UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70617</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:40.577077447UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70617</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:40.984762585UTC</td></tr><tr><td>65.109.23.55:17187</td><td>dymension_1100-1</td><td>STAVR-Archive 🟢</td><td>70618</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:47.462331085UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>70618</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:47.763727780UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70618</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:50.240367958UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70619</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:56.783925002UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>70619</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:28:57.453588234UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>70585</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:25:38.693969638UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>70595</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:37.515565283UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>70606</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:38.817055536UTC</td></tr><tr><td>78.47.67.0:26657</td><td>dymension_1100-1</td><td>bfxd 🟢</td><td>26001</td><td>26001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:58.624283966UTC</td></tr><tr><td>84.46.245.250:14657</td><td>dymension_1100-1</td><td>VNBNODE 🟢</td><td>70592</td><td>39843</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:18.281161529UTC</td></tr><tr><td>212.23.222.109:26757</td><td>dymension_1100-1</td><td>jaha_rpc 🟢</td><td>70597</td><td>40001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:26:46.875197031UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>70609</td><td>70001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T07:27:58.321604372UTC</td></tr></table>
