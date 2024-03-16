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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.30.14:26657</td><td>Oraichain</td><td>Mach5-Validators 🔴</td><td>16302792</td><td>0</td><td>False</td><td>off</td><td>212</td><td>2024-03-16T03:40:38.773648837UTC</td></tr><tr><td>35.237.59.125:26657</td><td>Oraichain</td><td>gcloud-sentry1 🟢</td><td>16302739</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:39:33.726595303UTC</td></tr><tr><td>34.148.48.252:26657</td><td>Oraichain</td><td>gcloud-sentry4 🟢</td><td>16302745</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:39:44.999412977UTC</td></tr><tr><td>3.134.19.98:26657</td><td>Oraichain</td><td>mainnet_sentry9 🟢</td><td>16302766</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:09.401785582UTC</td></tr><tr><td>34.138.129.148:26657</td><td>Oraichain</td><td>gcloud-sentry3 🟢</td><td>16302781</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:26.428571588UTC</td></tr><tr><td>3.21.106.169:26657</td><td>Oraichain</td><td>mainnet-light2 🟢</td><td>16302758</td><td>15275144</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:00.206129849UTC</td></tr><tr><td>3.146.152.67:26657</td><td>Oraichain</td><td>mainnet-light4 🟢</td><td>16302769</td><td>15275144</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:12.204449953UTC</td></tr><tr><td>3.135.200.149:26657</td><td>Oraichain</td><td>mainnet-light3 🟢</td><td>16302773</td><td>15275144</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:16.914322814UTC</td></tr><tr><td>18.221.220.160:26657</td><td>Oraichain</td><td>mainnet-light1 🟢</td><td>16302777</td><td>15643601</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:21.664990160UTC</td></tr><tr><td>65.21.15.100:36002</td><td>Oraichain</td><td>bricks_orai 🟢</td><td>16302796</td><td>15848470</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:43.235785302UTC</td></tr><tr><td>185.182.184.203:26657</td><td>Oraichain</td><td>PSnodes 🔴</td><td>16302743</td><td>15946937</td><td>False</td><td>off</td><td>27</td><td>2024-03-16T03:39:42.326084769UTC</td></tr><tr><td>75.119.130.219:26657</td><td>Oraichain</td><td>mortys_rpc 🟢</td><td>16302788</td><td>15960001</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:34.040060766UTC</td></tr><tr><td>37.27.96.218:26657</td><td>Oraichain</td><td>Strong_Node 🟢</td><td>16302800</td><td>16086201</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:47.677931087UTC</td></tr><tr><td>84.247.183.4:26657</td><td>Oraichain</td><td>oraiX1 🟢</td><td>16302800</td><td>16177601</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:47.985573510UTC</td></tr><tr><td>65.21.90.141:12301</td><td>Oraichain</td><td>SerGo 🔴</td><td>16302783</td><td>16202783</td><td>False</td><td>off</td><td>1</td><td>2024-03-16T03:40:28.837558974UTC</td></tr><tr><td>158.220.124.180:26657</td><td>Oraichain</td><td>ubik69_moniker-2 🔴</td><td>16302746</td><td>16229001</td><td>False</td><td>on</td><td>1815</td><td>2024-03-16T03:39:45.263849495UTC</td></tr><tr><td>213.199.49.203:26657</td><td>Oraichain</td><td>mam_orai_moniker 🔴</td><td>16302759</td><td>16268001</td><td>False</td><td>on</td><td>5</td><td>2024-03-16T03:40:00.488254052UTC</td></tr><tr><td>66.45.246.166:2057</td><td>Oraichain</td><td>STAVR-Service 🟢</td><td>16302788</td><td>16293101</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T03:40:33.647301161UTC</td></tr></table>
