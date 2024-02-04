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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.189.169.99:26657</td><td>Oraichain</td><td>ORAI_Vanguard_SENTRY 🟢</td><td>15613836</td><td>0</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T09:08:13.843438653UTC</td></tr><tr><td>23.106.238.179:26657</td><td>Oraichain</td><td>my_node 🔴</td><td>15613838</td><td>0</td><td>False</td><td>on</td><td>229722</td><td>2024-02-04T09:08:28.724502809UTC</td></tr><tr><td>5.78.98.175:26657</td><td>Oraichain</td><td>Nodes 🔴</td><td>15613840</td><td>0</td><td>False</td><td>off</td><td>164834</td><td>2024-02-04T09:08:39.009232333UTC</td></tr><tr><td>65.109.30.14:26657</td><td>Oraichain</td><td>Mach5-Validators 🔴</td><td>15613844</td><td>0</td><td>False</td><td>off</td><td>212</td><td>2024-02-04T09:09:03.221114704UTC</td></tr><tr><td>3.134.19.98:26657</td><td>Oraichain</td><td>mainnet_sentry4 🟢</td><td>15613839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T09:08:34.024222607UTC</td></tr><tr><td>46.4.23.225:26657</td><td>Oraichain</td><td>Blockval 🔴</td><td>15613845</td><td>10774049</td><td>False</td><td>off</td><td>278107</td><td>2024-02-04T09:09:08.003432962UTC</td></tr><tr><td>142.132.157.153:23357</td><td>Oraichain</td><td>345908-asgdlasdg 🟢</td><td>15613839</td><td>11956426</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T09:08:33.240635826UTC</td></tr><tr><td>65.108.232.168:33657</td><td>Oraichain</td><td>KonsorTech 🔴</td><td>15613835</td><td>14344801</td><td>False</td><td>off</td><td>50315</td><td>2024-02-04T09:08:09.377809331UTC</td></tr><tr><td>31.220.85.99:26657</td><td>Oraichain</td><td>ultra_node 🟢</td><td>15613845</td><td>15360001</td><td>False</td><td>off</td><td>0</td><td>2024-02-04T09:09:05.665539383UTC</td></tr><tr><td>65.21.90.141:12301</td><td>Oraichain</td><td>SerGo 🔴</td><td>15613843</td><td>15513843</td><td>False</td><td>off</td><td>1</td><td>2024-02-04T09:08:53.725939887UTC</td></tr><tr><td>66.45.246.166:2057</td><td>Oraichain</td><td>STAVR-Service 🟢</td><td>15613844</td><td>15529201</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T09:08:58.546672667UTC</td></tr></table>
