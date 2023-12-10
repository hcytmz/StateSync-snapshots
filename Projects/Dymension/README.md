<h1 align="center"> 🔥Dymension🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

<h1 align="center"> TESTNET</h1>

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
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Dymension-testnet/staking        `Indexer "ON"` \
🔥API🔥:          https://dymension.api.t.stavr.tech \
🔥RPC🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis🔥:     ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym```

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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>1641931</td><td>1</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:08.478690792UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>1641934</td><td>1</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:25.146640934UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>1641936</td><td>1</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:40.096088940UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>1641937</td><td>1</td><td>False</td><td>off</td><td>1</td><td>2023-12-10T20:27:46.024988236UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>1641931</td><td>106001</td><td>False</td><td>off</td><td>2</td><td>2023-12-10T20:27:09.210265407UTC</td></tr><tr><td>89.116.31.118:26657</td><td>froopyland_100-1</td><td>cardex 🟢</td><td>1641933</td><td>293001</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:27:17.807690805UTC</td></tr><tr><td>78.46.103.246:56657</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>1641930</td><td>407001</td><td>False</td><td>off</td><td>1</td><td>2023-12-10T20:27:02.650058657UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>1641935</td><td>591001</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:27:32.039418441UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>1641935</td><td>737456</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:32.498283095UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>1641935</td><td>737456</td><td>False</td><td>off</td><td>1</td><td>2023-12-10T20:27:32.955385069UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>1641928</td><td>820001</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:26:51.905307546UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>1641935</td><td>922548</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:33.300728765UTC</td></tr><tr><td>85.239.240.194:33657</td><td>froopyland_100-1</td><td>zardozmonopoly 🟢</td><td>1641939</td><td>935165</td><td>False</td><td>off</td><td>0</td><td>2023-12-10T20:27:55.632566278UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>1641936</td><td>1006001</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:39.750790693UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>1641938</td><td>1150548</td><td>False</td><td>off</td><td>1</td><td>2023-12-10T20:27:50.711781977UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1641928</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:26:48.328944650UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1641937</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2023-12-10T20:27:43.171486442UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>1641928</td><td>1330001</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:26:52.207664696UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>1641930</td><td>1341930</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:04.005242180UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>1641933</td><td>1341933</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:27:22.225422430UTC</td></tr><tr><td>194.163.185.53:14657</td><td>froopyland_100-1</td><td>megumii 🟢</td><td>1641930</td><td>1390788</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:27:03.615711228UTC</td></tr><tr><td>15.235.160.84:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>1641928</td><td>1435053</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:26:53.137590554UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🟢</td><td>1641937</td><td>1473622</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:27:46.353476327UTC</td></tr><tr><td>20.122.112.2:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1636516</td><td>1479282</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:26:57.865269043UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>1641935</td><td>1501386</td><td>False</td><td>off</td><td>1</td><td>2023-12-10T20:27:31.642868338UTC</td></tr><tr><td>144.91.65.13:26697</td><td>froopyland_100-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>1641930</td><td>1561776</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:27:03.271267151UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>1641937</td><td>1561776</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:45.744011931UTC</td></tr><tr><td>38.242.151.229:33657</td><td>froopyland_100-1</td><td>salomonval 🟢</td><td>1641936</td><td>1569001</td><td>False</td><td>off</td><td>0</td><td>2023-12-10T20:27:40.510613090UTC</td></tr><tr><td>37.27.54.228:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>1641937</td><td>1589489</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:42.885174975UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>1641928</td><td>1620621</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:26:48.965662825UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>1641929</td><td>1637277</td><td>False</td><td>on</td><td>0</td><td>2023-12-10T20:26:58.303185198UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>1641933</td><td>1640001</td><td>False</td><td>on</td><td>1</td><td>2023-12-10T20:27:22.652511828UTC</td></tr></table>
