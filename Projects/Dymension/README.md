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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>2446122</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:02:02.822861863UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:00:53.046673428UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-02-05T15:02:01.885426184UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>2446112</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:00:57.492160975UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>2446115</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:16.339402856UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>2446115</td><td>1652923</td><td>False</td><td>off</td><td>3</td><td>2024-02-05T15:01:17.053532156UTC</td></tr><tr><td>65.108.196.205:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>2446119</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:01:40.070886904UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>2446120</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:48.171246295UTC</td></tr><tr><td>46.4.99.152:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>2446120</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:01:50.547926754UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>2446121</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:57.038790720UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>2446124</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-02-05T15:02:09.778636790UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>2446122</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:57.455248607UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>2446124</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:02:09.521584743UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>2446112</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:00:57.815145792UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>2446119</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:43.151086526UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>2446120</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-02-05T15:01:47.904811795UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🔴</td><td>2446124</td><td>1723012</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:02:10.169204661UTC</td></tr><tr><td>194.233.90.134:26657</td><td>froopyland_100-1</td><td>geonodes 🔴</td><td>2446117</td><td>2015001</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:33.490483932UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>2446124</td><td>2060558</td><td>False</td><td>off</td><td>1</td><td>2024-02-05T15:02:14.581610583UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>2446119</td><td>2077398</td><td>False</td><td>off</td><td>1</td><td>2024-02-05T15:01:40.356228336UTC</td></tr><tr><td>65.21.73.18:30657</td><td>froopyland_100-1</td><td>ST-Server 🔴</td><td>2446111</td><td>2082417</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:00:54.124825325UTC</td></tr><tr><td>167.235.9.223:61557</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>2446116</td><td>2100380</td><td>False</td><td>off</td><td>1</td><td>2024-02-05T15:01:21.535370815UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>2446114</td><td>2146114</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:09.452282248UTC</td></tr><tr><td>152.53.16.17:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>2446112</td><td>2169800</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:00:56.573675509UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🔴</td><td>2446113</td><td>2225118</td><td>False</td><td>on</td><td>2</td><td>2024-02-05T15:01:03.746663406UTC</td></tr><tr><td>89.116.31.118:26657</td><td>froopyland_100-1</td><td>cardex 🟢</td><td>2446116</td><td>2339417</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:01:28.037860853UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>2446111</td><td>2339618</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:00:53.747526795UTC</td></tr><tr><td>65.109.64.99:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>2446114</td><td>2339618</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:01:13.946019778UTC</td></tr><tr><td>139.162.59.83:26657</td><td>froopyland_100-1</td><td>z3z 🟢</td><td>2446112</td><td>2374973</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:01:01.230922576UTC</td></tr><tr><td>202.8.8.145:26657</td><td>froopyland_100-1</td><td>twinstake 🔴</td><td>2446120</td><td>2384116</td><td>False</td><td>off</td><td>1</td><td>2024-02-05T15:01:47.560911521UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>2446117</td><td>2432923</td><td>False</td><td>on</td><td>1</td><td>2024-02-05T15:01:32.492204875UTC</td></tr><tr><td>144.91.65.13:26697</td><td>froopyland_100-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>2445925</td><td>2433739</td><td>False</td><td>on</td><td>0</td><td>2024-02-05T15:01:09.038304050UTC</td></tr></table>
