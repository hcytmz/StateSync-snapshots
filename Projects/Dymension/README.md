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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>3497</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:00.313124398UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3497</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:03.091318612UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>3497</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:03.861258541UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>3497</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:04.243068645UTC</td></tr><tr><td>5.78.103.84:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3498</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:05.246576347UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3498</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:05.603209299UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>3498</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:06.262290357UTC</td></tr><tr><td>95.216.142.40:26657</td><td>dymension_1100-1</td><td>inklbot 🟢</td><td>3498</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:10.714764936UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>3499</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:13.088477254UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3500</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:17.463628969UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3501</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:28.044280673UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3501</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:28.986199874UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>3502</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:29.403406865UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3502</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:31.864399801UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3502</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:32.773962419UTC</td></tr><tr><td>45.76.86.41:26657</td><td>dymension_1100-1</td><td>KudasaiJP 🔴</td><td>3502</td><td>1</td><td>False</td><td>on</td><td>60207</td><td>2024-02-06T19:34:35.113186697UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>3503</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:37.535387351UTC</td></tr><tr><td>5.78.111.114:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3503</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:40.547972263UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3503</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:40.935092436UTC</td></tr><tr><td>91.107.208.199:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3503</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:41.236955063UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>3503</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:41.570290689UTC</td></tr><tr><td>144.91.68.181:26657</td><td>dymension_1100-1</td><td>vmi1526870.contaboserver.net 🟢</td><td>3504</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:41.868165450UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>3504</td><td>1</td><td>False</td><td>off</td><td>152488</td><td>2024-02-06T19:34:44.369613368UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3504</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:45.282020520UTC</td></tr><tr><td>167.235.9.223:61657</td><td>dymension_1100-1</td><td>F5Nodes 🟢</td><td>1</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-06T19:34:47.645530499UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3505</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:48.009906501UTC</td></tr><tr><td>49.13.63.87:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3505</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:48.298578274UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>3505</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:52.735468725UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3507</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:01.210214824UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3507</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:01.699753751UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3507</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:04.086234975UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>3508</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:06.413587764UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>3508</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:10.796560542UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>3508</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:11.065104611UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3509</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:15.452394224UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3509</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:17.781173498UTC</td></tr><tr><td>5.161.103.111:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3510</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:20.802166301UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3510</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:21.086147648UTC</td></tr><tr><td>5.78.84.136:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3510</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:22.010786378UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3511</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:24.453434858UTC</td></tr><tr><td>5.78.98.90:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3511</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:29.572486573UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3512</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:31.977310396UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3513</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:36.466454376UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3513</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:39.285995651UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>3513</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:41.642360255UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3514</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:42.563542914UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3514</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:47.013279028UTC</td></tr><tr><td>5.78.114.208:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3514</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:48.029614247UTC</td></tr><tr><td>5.78.68.191:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3515</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:49.067562925UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3515</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:51.824564738UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>3515</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:54.208511101UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3516</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:55.218941848UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3516</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:55.596371078UTC</td></tr><tr><td>49.13.133.97:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3518</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:08.276063761UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>3518</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:08.643054849UTC</td></tr><tr><td>5.78.114.153:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3518</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:11.714489504UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3519</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:14.209399196UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>3522</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:37.137547421UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3523</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:39.588303077UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3524</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:44.030393471UTC</td></tr><tr><td>5.78.94.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3524</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:44.965912336UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3524</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:45.792894182UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3524</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:48.165354400UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3524</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:48.530893274UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>3525</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:52.972594549UTC</td></tr><tr><td>5.78.95.189:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3525</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:53.920189007UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3526</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:56.245027055UTC</td></tr><tr><td>5.78.81.63:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3526</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:36:59.224976391UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>3526</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:37:01.651469020UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3527</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:37:02.085942190UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3527</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:37:02.782964839UTC</td></tr><tr><td>5.75.239.133:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>3527</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:37:03.074410264UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>3497</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:34:03.481683548UTC</td></tr><tr><td>37.27.59.176:14657</td><td>dymension_1100-1</td><td>luciolaKami 🟢</td><td>3513</td><td>383</td><td>False</td><td>on</td><td>0</td><td>2024-02-06T19:35:38.865732941UTC</td></tr></table>
