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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>75835</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:43:57.947436961UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75836</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:02.689681559UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>75836</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:03.475399208UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>75836</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:03.877596283UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75836</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:04.225160330UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>75837</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:04.907158318UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75837</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:07.233705905UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>75837</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:10.085182856UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>75838</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:12.411402799UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75838</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:14.809481945UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75841</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:29.617569834UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75841</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:32.593086188UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>75841</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:33.054497418UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:35.484151398UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:36.402243749UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>75842</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:40.948070653UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>75843</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:41.396885825UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>75843</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:42.294247718UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75843</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:45.085000441UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>75843</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:45.416076305UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>75843</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:46.500349091UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>75844</td><td>1</td><td>False</td><td>off</td><td>622842</td><td>2024-02-11T15:44:49.035588322UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75845</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:49.914828325UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75845</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:54.560351989UTC</td></tr><tr><td>65.21.229.60:37657</td><td>dymension_1100-1</td><td>r-index-bh 🟢</td><td>75846</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:56.959292841UTC</td></tr><tr><td>75.119.139.53:26667</td><td>dymension_1100-1</td><td>AVIAONE_Blockchains_Service 🟢</td><td>75847</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:01.444059679UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75848</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:08.475978553UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75848</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:10.897437425UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>75849</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:13.728243919UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>75849</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-11T15:45:18.220357481UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>75850</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:20.562987532UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75850</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:22.869032495UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75851</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:25.502803379UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75851</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:27.850425850UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75852</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:34.449100646UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75854</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:47.193181384UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75855</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:53.810100737UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75856</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:56.253610184UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>75857</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:00.743188752UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75858</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:05.191380702UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75858</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:06.596024810UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>75858</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:09.013409543UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75859</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:09.962050712UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>75859</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-11T15:46:10.444527620UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75862</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:32.045377426UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>75866</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:54.959405500UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75866</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:57.503779786UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>75867</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:59.940957251UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75867</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:04.431236180UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75868</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:05.096794885UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75869</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:07.527400786UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75869</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:07.987065331UTC</td></tr><tr><td>65.109.23.55:17187</td><td>dymension_1100-1</td><td>STAVR-Archive 🟢</td><td>75870</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:14.531218907UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>75870</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:14.867479952UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75870</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:15.316191079UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>75871</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:23.815971248UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75871</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:24.169850947UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>75872</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:47:24.788717765UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>75836</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:03.059960326UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>75847</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:01.834462399UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>75858</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:05.516292376UTC</td></tr><tr><td>78.47.67.0:26657</td><td>dymension_1100-1</td><td>bfxd 🟢</td><td>26001</td><td>26001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:23.154959244UTC</td></tr><tr><td>84.46.245.250:14657</td><td>dymension_1100-1</td><td>VNBNODE 🟢</td><td>75843</td><td>39843</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:44:42.607531480UTC</td></tr><tr><td>212.23.222.109:26757</td><td>dymension_1100-1</td><td>jaha_rpc 🟢</td><td>75848</td><td>40001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:45:11.273919614UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>75861</td><td>73001</td><td>False</td><td>on</td><td>0</td><td>2024-02-11T15:46:25.414894161UTC</td></tr></table>
