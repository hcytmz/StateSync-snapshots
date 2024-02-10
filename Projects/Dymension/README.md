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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>65328</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:30.981058837UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65334</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:35.780399225UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>65334</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:36.652982314UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65334</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:37.058461104UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>65334</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:37.723052121UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65335</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:40.068248170UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>65335</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:42.976989959UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>65336</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:45.302663492UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65336</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:47.793186369UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65339</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:02.474127439UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65339</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:03.331921394UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>65339</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:03.675908691UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65340</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:06.223686422UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65340</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:09.241394768UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>65341</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:13.733733157UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>65341</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:14.233187937UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>65341</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:15.231571295UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65342</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:17.973472891UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>65342</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:18.257119941UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>65342</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:19.380342034UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>65342</td><td>1</td><td>False</td><td>off</td><td>621553</td><td>2024-02-10T23:08:21.757231156UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65343</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:22.687626427UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65343</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:27.467262833UTC</td></tr><tr><td>65.21.229.60:37657</td><td>dymension_1100-1</td><td>r-index-bh 🟢</td><td>65344</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:29.943321307UTC</td></tr><tr><td>75.119.139.53:26667</td><td>dymension_1100-1</td><td>AVIAONE_Blockchains_Service 🟢</td><td>65344</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:34.479096897UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65346</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:41.400227716UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65346</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:43.821401502UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>65346</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:46.559657792UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>65347</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-10T23:08:51.013283419UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>65348</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:55.429157769UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65348</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:55.677171873UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65348</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:58.289634958UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65349</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:00.704067493UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65350</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:05.123928128UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65352</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:17.894577878UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65353</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:24.529820977UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65354</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:26.901544203UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>65355</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:31.343371046UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65355</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:35.831427697UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65355</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:36.569384596UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>65356</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:39.021242054UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65356</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:09:40.042254448UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>65356</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-10T23:09:40.464890489UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65360</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:01.907431355UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>65364</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:24.917415163UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65365</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:27.313653026UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>65365</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:29.798471678UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65366</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:34.273365536UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65366</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:34.899653438UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65366</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:37.357384870UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65366</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:37.780008956UTC</td></tr><tr><td>65.109.23.55:17187</td><td>dymension_1100-1</td><td>STAVR-Archive 🟢</td><td>65367</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:44.336064009UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>65367</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:44.605965696UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65367</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:45.090567257UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>65369</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:53.627084533UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65369</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:54.038371916UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>65369</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:10:54.683095013UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>65334</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:07:36.208719601UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>65345</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:34.829102037UTC</td></tr><tr><td>78.47.67.0:26657</td><td>dymension_1100-1</td><td>bfxd 🟢</td><td>26001</td><td>26001</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:55.940139281UTC</td></tr><tr><td>84.46.245.250:14657</td><td>dymension_1100-1</td><td>VNBNODE 🟢</td><td>65341</td><td>39843</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:15.590347192UTC</td></tr><tr><td>212.23.222.109:26757</td><td>dymension_1100-1</td><td>jaha_rpc 🟢</td><td>65346</td><td>40001</td><td>False</td><td>on</td><td>0</td><td>2024-02-10T23:08:44.242723253UTC</td></tr></table>
