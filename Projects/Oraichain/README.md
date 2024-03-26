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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.30.14:26657</td><td>Oraichain</td><td>Mach5-Validators 🔴</td><td>17005436</td><td>0</td><td>False</td><td>off</td><td>212</td><td>2024-03-26T05:20:39.578077494UTC</td></tr><tr><td>65.109.70.38:26657</td><td>Oraichain</td><td>Junkers 🔴</td><td>17005448</td><td>0</td><td>False</td><td>off</td><td>196431</td><td>2024-03-26T05:20:53.049659891UTC</td></tr><tr><td>3.134.19.98:26657</td><td>Oraichain</td><td>mainnet-sentry9 🟢</td><td>17005407</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:08.289463864UTC</td></tr><tr><td>34.138.129.148:26657</td><td>Oraichain</td><td>gcloud-sentry3 🟢</td><td>17005423</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:25.242057971UTC</td></tr><tr><td>34.148.71.71:26657</td><td>Oraichain</td><td>gcloud-sentry4 🟢</td><td>17005430</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:32.707042287UTC</td></tr><tr><td>65.21.15.100:36002</td><td>Oraichain</td><td>bricks_orai 🟢</td><td>17005440</td><td>15848470</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:44.180544477UTC</td></tr><tr><td>75.119.130.219:26657</td><td>Oraichain</td><td>mortys_rpc 🟢</td><td>17005430</td><td>15960001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:33.033699301UTC</td></tr><tr><td>84.247.183.4:26657</td><td>Oraichain</td><td>oraiX1 🟢</td><td>17002366</td><td>16177601</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:46.594277037UTC</td></tr><tr><td>213.199.49.203:26657</td><td>Oraichain</td><td>mam_orai_moniker 🔴</td><td>17005404</td><td>16268001</td><td>False</td><td>on</td><td>8</td><td>2024-03-26T05:20:00.609325424UTC</td></tr><tr><td>213.199.54.195:26657</td><td>Oraichain</td><td>ubik69_moniker 🔴</td><td>17005387</td><td>16400001</td><td>False</td><td>on</td><td>1830</td><td>2024-03-26T05:19:41.267657959UTC</td></tr><tr><td>3.21.106.169:26657</td><td>Oraichain</td><td>mainnet-light2 🟢</td><td>17005404</td><td>16436001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:00.314613656UTC</td></tr><tr><td>3.146.152.67:26657</td><td>Oraichain</td><td>mainnet-light4 🟢</td><td>17005408</td><td>16436001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:08.911563562UTC</td></tr><tr><td>3.135.200.149:26657</td><td>Oraichain</td><td>mainnet-light3 🟢</td><td>17005414</td><td>16436001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:15.773053049UTC</td></tr><tr><td>18.221.220.160:26657</td><td>Oraichain</td><td>mainnet-light4 🟢</td><td>17005418</td><td>16588001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:20.498162170UTC</td></tr><tr><td>18.198.141.150:26657</td><td>Oraichain</td><td>oraichain-validator-01 🔴</td><td>17005436</td><td>16650390</td><td>False</td><td>on</td><td>32574</td><td>2024-03-26T05:20:39.797686947UTC</td></tr><tr><td>66.45.246.166:2057</td><td>Oraichain</td><td>STAVR-Service 🟢</td><td>17001010</td><td>16987001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T05:20:32.095802881UTC</td></tr></table>
