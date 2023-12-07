<h1 align="center"> 🔥Ojo🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Ojo)
=

<h1 align="center"> TESTNET</h1>

# StateSync Ojo Testnet
```python
SNAP_RPC=http://ojo.rpc.t.stavr.tech:37097
peers="1f091cf9567c0d72a0f93877007379e0298b8860@ojo.peer.stavr.tech:37096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.ojo/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.ojo/config/config.toml
ojod tendermint unsafe-reset-all --home /root/.ojo --keep-addr-book
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.ojo/config/app.toml
sudo systemctl restart ojod && journalctl -u ojod -f -o cat
```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop ojod
cp $HOME/.ojo/data/priv_validator_state.json $HOME/.ojo/priv_validator_state.json.backup
rm -rf $HOME/.ojo/data
curl -o - -L http://ojo.snapshot.stavr.tech:1026/ojo/ojo-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ojo --strip-components 2
mv $HOME/.ojo/priv_validator_state.json.backup $HOME/.ojo/data/priv_validator_state.json
wget -O $HOME/.ojo/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/addrbook.json"
sudo systemctl restart ojod && journalctl -u ojod -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:        https://explorer.stavr.tech/Ojo-Devnet/staking        `Indexer "ON"` \
🔥API🔥:                     https://ojo.api.t.stavr.tech \
🔥RPC🔥:                    http://ojo.rpc.t.stavr.tech:37097              `Snapshot-interval = 100` \
🔥gRPC🔥:                  http://ojo.grpc.t.stavr.tech:7729 \
🔥peer🔥:                   `1f091cf9567c0d72a0f93877007379e0298b8860@ojo.peer.stavr.tech:37096` \
🔥Genesis🔥:    ```wget -O $HOME/.ojo/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/genesis.json"``` \
🔥Addrbook🔥:    ```wget -O $HOME/.ojo/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O ojjo https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/ojjo && chmod +x ojjo && ./ojjo```


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

[raw json Testnet](https://rpc-check.ojot.stavr.tech/ojot/rpc-ojot-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>88.198.32.17:39657</td><td>ojo-devnet</td><td>node 🔴</td><td>4376060</td><td>300001</td><td>False</td><td>on</td><td>65654</td><td>2023-12-07T07:15:04.019056544UTC</td></tr><tr><td>65.108.199.120:54657</td><td>ojo-devnet</td><td>RAMZES 🔴</td><td>4376055</td><td>306156</td><td>False</td><td>on</td><td>15420</td><td>2023-12-07T07:14:37.627040239UTC</td></tr><tr><td>136.243.88.91:7331</td><td>ojo-devnet</td><td>ojo_testnet 🔴</td><td>4376056</td><td>308845</td><td>False</td><td>on</td><td>1000</td><td>2023-12-07T07:14:44.216404932UTC</td></tr><tr><td>142.132.209.236:21657</td><td>ojo-devnet</td><td>node 🔴</td><td>4376060</td><td>350001</td><td>False</td><td>on</td><td>1999</td><td>2023-12-07T07:15:02.810781743UTC</td></tr><tr><td>65.109.70.45:16657</td><td>ojo-devnet</td><td>L0vd.com 🔴</td><td>4376061</td><td>695918</td><td>False</td><td>off</td><td>998</td><td>2023-12-07T07:15:09.769627084UTC</td></tr><tr><td>65.109.93.152:33657</td><td>ojo-devnet</td><td>AlxVoy 🔴</td><td>4376060</td><td>2319801</td><td>False</td><td>on</td><td>4536782</td><td>2023-12-07T07:15:02.570004745UTC</td></tr><tr><td>51.159.220.202:26657</td><td>ojo-devnet</td><td>Blockscope.net 🔴</td><td>4376055</td><td>2658001</td><td>False</td><td>on</td><td>981</td><td>2023-12-07T07:14:36.846892893UTC</td></tr><tr><td>213.239.207.175:47657</td><td>ojo-devnet</td><td>landeros 🔴</td><td>4376059</td><td>2714001</td><td>False</td><td>off</td><td>11083</td><td>2023-12-07T07:14:57.810199032UTC</td></tr><tr><td>158.220.92.97:26677</td><td>ojo-devnet</td><td>AVIAONE 🔴</td><td>4376059</td><td>2754001</td><td>False</td><td>on</td><td>13867</td><td>2023-12-07T07:14:57.499997407UTC</td></tr><tr><td>77.54.1.75:1203</td><td>ojo-devnet</td><td>don 🔴</td><td>4376060</td><td>2906401</td><td>False</td><td>on</td><td>10</td><td>2023-12-07T07:15:03.678668875UTC</td></tr><tr><td>95.217.225.212:36657</td><td>ojo-devnet</td><td>Firstcome 🔴</td><td>4376056</td><td>2985946</td><td>False</td><td>on</td><td>13566</td><td>2023-12-07T07:14:43.974242741UTC</td></tr><tr><td>213.239.194.132:50657</td><td>ojo-devnet</td><td>semalist 🔴</td><td>4376055</td><td>3223522</td><td>False</td><td>on</td><td>19037</td><td>2023-12-07T07:14:37.918718102UTC</td></tr><tr><td>95.217.224.252:19657</td><td>ojo-devnet</td><td>Galaxynode 🔴</td><td>4376060</td><td>3685492</td><td>False</td><td>on</td><td>11888</td><td>2023-12-07T07:15:06.677732164UTC</td></tr><tr><td>178.159.5.187:60657</td><td>ojo-devnet</td><td>x0ser 🔴</td><td>4284267</td><td>3940946</td><td>False</td><td>off</td><td>9764</td><td>2023-12-07T07:14:44.584624125UTC</td></tr><tr><td>65.108.238.61:20657</td><td>ojo-devnet</td><td>alex 🔴</td><td>4376055</td><td>4158001</td><td>False</td><td>on</td><td>11359</td><td>2023-12-07T07:14:37.278789263UTC</td></tr><tr><td>38.242.237.5:12657</td><td>ojo-devnet</td><td>oibek 🔴</td><td>4376055</td><td>4196001</td><td>False</td><td>off</td><td>1008</td><td>2023-12-07T07:14:38.283747366UTC</td></tr><tr><td>62.171.182.164:12657</td><td>ojo-devnet</td><td>zkhumo 🔴</td><td>4375577</td><td>4196001</td><td>False</td><td>off</td><td>999</td><td>2023-12-07T07:15:03.160953896UTC</td></tr><tr><td>78.46.99.50:22657</td><td>ojo-devnet</td><td>Staketab 🔴</td><td>4376061</td><td>4254801</td><td>False</td><td>on</td><td>1276</td><td>2023-12-07T07:15:10.011784573UTC</td></tr><tr><td>142.132.134.112:25357</td><td>ojo-devnet</td><td>Pro-Nodes75 🔴</td><td>4376056</td><td>4276056</td><td>False</td><td>on</td><td>24651</td><td>2023-12-07T07:14:41.266776154UTC</td></tr><tr><td>65.21.170.3:38657</td><td>ojo-devnet</td><td>Munris 🔴</td><td>4376056</td><td>4276056</td><td>False</td><td>off</td><td>20123</td><td>2023-12-07T07:14:43.623768690UTC</td></tr><tr><td>173.212.222.167:30657</td><td>ojo-devnet</td><td>moodman 🟢</td><td>4376058</td><td>4276058</td><td>False</td><td>off</td><td>0</td><td>2023-12-07T07:14:55.063273328UTC</td></tr><tr><td>65.108.227.112:15057</td><td>ojo-devnet</td><td>[NODERS]TEAM 🔴</td><td>4376061</td><td>4276060</td><td>False</td><td>off</td><td>9999</td><td>2023-12-07T07:15:07.027707327UTC</td></tr><tr><td>138.201.85.176:26697</td><td>ojo-devnet</td><td>ojo-devnet 🔴</td><td>4376061</td><td>4276061</td><td>False</td><td>on</td><td>1000024000</td><td>2023-12-07T07:15:09.445543782UTC</td></tr><tr><td>135.181.210.171:37097</td><td>ojo-devnet</td><td>STAVR-Service 🟢</td><td>4376055</td><td>4373001</td><td>False</td><td>on</td><td>0</td><td>2023-12-07T07:14:38.915570324UTC</td></tr></table>