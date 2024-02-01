<h1 align="center"> 🔥XPLA🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Xpla)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://xpla.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.xpla/config/config.toml
xplad tendermint unsafe-reset-all
wget -O $HOME/.xpla/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Xpla/addrbook.json"
curl -o - -L https://xpla.wasm.stavr.tech/wasm-xpla.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.xpla --strip-components 2
sudo systemctl restart xplad && sudo journalctl -u xplad -f -o cat
```
# SnapShot (~2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop xplad
cp $HOME/.xpla/data/priv_validator_state.json $HOME/.xpla/priv_validator_state.json.backup
rm -rf $HOME/.xpla/data
curl -o - -L https://xpla.snapshot.stavr.tech/xpla/xpla-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.xpla --strip-components 2
mv $HOME/.xpla/priv_validator_state.json.backup $HOME/.xpla/data/priv_validator_state.json
wget -O $HOME/.xpla/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Xpla/addrbook.json"
sudo systemctl restart xplad && journalctl -u xplad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Xpla-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://xpla.api.m.stavr.tech \
🔥RPC🔥:          https://xpla.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://xpla.grpc.m.stavr.tech:112 \
🔥EVMRPC🔥:       http://xpla.evm-rpc.m.stavr.tech \
🔥seed🔥:      `466c9c2e8b128389059bf4e7e68888fdde8cbebc@xpla.seed.stavr.tech:2066` \
🔥Genesis🔥:   `wget -O $HOME/.xpla/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Xpla/genesis.json"` \
🔥WASM🔥:      `curl -o - -L https://xpla.wasm.stavr.tech/wasm-xpla.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.xpla --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.xpla/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Xpla/addrbook.json"` \
🔥Auto_install script🔥:`wget -O xplam https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Xpla/xplam && chmod +x xplam && ./xplam`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Xpla/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.xplam.stavr.tech/xplam/rpc-xplam-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>116.202.109.80:26657</td><td>dimension_37-1</td><td>venly-xpla-sentry-1 🟢</td><td>7518180</td><td>0</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:42:41.374800943UTC</td></tr><tr><td>5.75.233.114:26657</td><td>dimension_37-1</td><td>venly-xpla-sentry-2 🟢</td><td>7518186</td><td>0</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:20.226430086UTC</td></tr><tr><td>35.225.31.157:26657</td><td>dimension_37-1</td><td>xpla-node03.c.h-live.internal 🟢</td><td>7518185</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:09.556440100UTC</td></tr><tr><td>34.86.128.71:26657</td><td>dimension_37-1</td><td>HOLDINGS_SEN01 🟢</td><td>7518185</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:12.323259178UTC</td></tr><tr><td>35.245.222.190:26657</td><td>dimension_37-1</td><td>HOLDINGS_SEN02 🟢</td><td>7518186</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:19.146429406UTC</td></tr><tr><td>35.188.20.172:26657</td><td>dimension_37-1</td><td>xpla_node_02 🟢</td><td>7518186</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:19.905407959UTC</td></tr><tr><td>34.85.122.216:26657</td><td>dimension_37-1</td><td>zenaad-collector 🟢</td><td>7518189</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:37.886058035UTC</td></tr><tr><td>34.142.251.87:26657</td><td>dimension_37-1</td><td>CrossnodeLabs_SEN02 🟢</td><td>7518192</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:52.176453322UTC</td></tr><tr><td>34.87.100.83:26657</td><td>dimension_37-1</td><td>CrossnodeLabs_SEN01 🟢</td><td>7518194</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:08.182583497UTC</td></tr><tr><td>34.145.148.128:26657</td><td>dimension_37-1</td><td>xpla_node_02 🟢</td><td>7518195</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:10.920736709UTC</td></tr><tr><td>104.197.217.143:26657</td><td>dimension_37-1</td><td>xpla-node03.c.h-live.internal 🟢</td><td>7518196</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:16.194254701UTC</td></tr><tr><td>65.108.45.172:36657</td><td>dimension_37-1</td><td>Moonlet 🟢</td><td>7518197</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:23.587685727UTC</td></tr><tr><td>3.254.166.145:26657</td><td>dimension_37-1</td><td>m-xpla-01 🟢</td><td>7518184</td><td>4878569</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:43:08.855298677UTC</td></tr><tr><td>165.22.228.158:26657</td><td>dimension_37-1</td><td>Figment 🟢</td><td>7518193</td><td>5942092</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:01.129194154UTC</td></tr><tr><td>147.182.146.152:26657</td><td>dimension_37-1</td><td>Figment 🟢</td><td>7518197</td><td>5942092</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:23.246854614UTC</td></tr><tr><td>95.168.173.33:36657</td><td>dimension_37-1</td><td>XPLA-mainnet-prod 🔴</td><td>7518196</td><td>7268196</td><td>False</td><td>on</td><td>1175</td><td>2024-02-01T03:44:20.538356397UTC</td></tr><tr><td>135.181.210.171:2067</td><td>dimension_37-1</td><td>STAVR-Service 🟢</td><td>7518195</td><td>7516001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T03:44:13.417521170UTC</td></tr><tr><td>54.183.210.199:26657</td><td>dimension_37-1</td><td>B-Harvest 🟢</td><td>7518190</td><td>7518045</td><td>False</td><td>off</td><td>0</td><td>2024-02-01T03:43:40.882152298UTC</td></tr></table>