<h1 align="center"> 🔥Oraichain🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Oraichain)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://orai.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.oraid/config/config.toml
oraid tendermint unsafe-reset-all
wget -O $HOME/.oraid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Oraichain/addrbook.json"
curl -o - -L https://orai.wasm.stavr.tech/wasm-orai.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.oraid --strip-components 2
sudo systemctl restart oraid && sudo journalctl -u oraid -f -o cat
```
# SnapShot (~2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop oraid
cp $HOME/.oraid/data/priv_validator_state.json $HOME/.oraid/priv_validator_state.json.backup
rm -rf $HOME/.oraid/data
curl -o - -L https://orai.snapshot.stavr.tech/oraid/oraid-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.oraid --strip-components 2
curl -o - -L https://orai.wasm.stavr.tech/wasm-orai.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.oraid --strip-components 2
mv $HOME/.oraid/priv_validator_state.json.backup $HOME/.oraid/data/priv_validator_state.json
wget -O $HOME/.oraid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Oraichain/addrbook.json"
sudo systemctl restart oraid && journalctl -u oraid -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Orai-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://orai.api.m.stavr.tech \
🔥RPC🔥:          https://orai.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://orai.grpc.m.stavr.tech:110 \
🔥seed🔥:      `4babdcd4c81d589e789db3b294eebcd779f2227c@orai.seed.stavr.tech:2056` \
🔥Genesis🔥:   `wget -O $HOME/.oraid/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Oraichain/genesis.json"` \
🔥WASM🔥:      `curl -o - -L https://orai.wasm.stavr.tech/wasm-orai.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.oraid --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.oraid/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Oraichain/addrbook.json"` \
🔥Auto_install script🔥:`wget -O oraim https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Oraichain/oraim && chmod +x oraim && ./oraim`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Oraichain/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.oraim.stavr.tech/oraim/rpc-oraim-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.189.169.99:26657</td><td>Oraichain</td><td>ORAI_Vanguard_SENTRY 🟢</td><td>16044993</td><td>0</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:36:58.494425418UTC</td></tr><tr><td>5.78.98.175:26657</td><td>Oraichain</td><td>Nodes 🔴</td><td>16044999</td><td>0</td><td>False</td><td>off</td><td>166122</td><td>2024-03-03T22:37:30.603590608UTC</td></tr><tr><td>65.109.30.14:26657</td><td>Oraichain</td><td>Mach5-Validators 🔴</td><td>16045003</td><td>0</td><td>False</td><td>off</td><td>644</td><td>2024-03-03T22:37:53.212726042UTC</td></tr><tr><td>35.237.59.125:26657</td><td>Oraichain</td><td>gcloud-sentry1 🟢</td><td>16044993</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:36:55.612678524UTC</td></tr><tr><td>3.134.19.98:26657</td><td>Oraichain</td><td>mainnet_sentry9 🟢</td><td>16044998</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:24.917873676UTC</td></tr><tr><td>34.138.129.148:26657</td><td>Oraichain</td><td>gcloud-sentry3 🟢</td><td>16045001</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:41.074622855UTC</td></tr><tr><td>62.171.174.124:26657</td><td>Oraichain</td><td>mortys_node 🔴</td><td>16045003</td><td>1</td><td>False</td><td>off</td><td>168575</td><td>2024-03-03T22:37:53.504261598UTC</td></tr><tr><td>46.4.23.225:26657</td><td>Oraichain</td><td>Blockval 🔴</td><td>16045004</td><td>10774049</td><td>False</td><td>off</td><td>276971</td><td>2024-03-03T22:37:58.244043808UTC</td></tr><tr><td>65.108.232.168:33657</td><td>Oraichain</td><td>KonsorTech 🔴</td><td>16044993</td><td>14344801</td><td>False</td><td>off</td><td>50588</td><td>2024-03-03T22:36:54.989403468UTC</td></tr><tr><td>3.21.106.169:26657</td><td>Oraichain</td><td>mainnet-light2 🟢</td><td>16044997</td><td>15275144</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:17.845655522UTC</td></tr><tr><td>3.146.152.67:26657</td><td>Oraichain</td><td>mainnet-light4 🟢</td><td>16044999</td><td>15275144</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:29.647974156UTC</td></tr><tr><td>3.135.200.149:26657</td><td>Oraichain</td><td>mainnet-light3 🟢</td><td>16045000</td><td>15275144</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:33.307191426UTC</td></tr><tr><td>18.221.220.160:26657</td><td>Oraichain</td><td>mainnet-light1 🟢</td><td>16045001</td><td>15643601</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:38.028384572UTC</td></tr><tr><td>65.21.15.100:36002</td><td>Oraichain</td><td>bricks_orai 🟢</td><td>16045004</td><td>15848470</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:58.035165118UTC</td></tr><tr><td>65.21.90.141:12301</td><td>Oraichain</td><td>SerGo 🔴</td><td>16045002</td><td>15945002</td><td>False</td><td>off</td><td>1</td><td>2024-03-03T22:37:43.453679409UTC</td></tr><tr><td>89.117.51.135:26657</td><td>Oraichain</td><td>mam_orai_moniker 🔴</td><td>16044993</td><td>15951001</td><td>False</td><td>on</td><td>5</td><td>2024-03-03T22:36:55.930366990UTC</td></tr><tr><td>75.119.130.219:26657</td><td>Oraichain</td><td>mortys_rpc 🟢</td><td>16045003</td><td>15960001</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:48.562015816UTC</td></tr><tr><td>109.199.126.132:26657</td><td>Oraichain</td><td>PSnodes 🔴</td><td>16045001</td><td>15964001</td><td>False</td><td>on</td><td>21</td><td>2024-03-03T22:37:38.316627045UTC</td></tr><tr><td>135.181.31.169:26657</td><td>Oraichain</td><td>Strong_Node 🟢</td><td>16044110</td><td>16025001</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:17.183145272UTC</td></tr><tr><td>66.45.246.166:2057</td><td>Oraichain</td><td>STAVR-Service 🟢</td><td>16045002</td><td>16041201</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T22:37:48.202209429UTC</td></tr></table>
