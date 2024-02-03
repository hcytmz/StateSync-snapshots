<h1 align="center"> 🔥Lum Network🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Lum)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://lum.rpc.m.stavr.tech:443
SEEDS=42d79514ca40e942004e94f90557644cf36e986a@lum.seed.stavr.tech:31316
cp $HOME/.lumd/data/priv_validator_state.json $HOME/.lumd/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.lumd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.lumd/config/config.toml
lumd tendermint unsafe-reset-all --home $HOME/.lumd --keep-addr-book
mv $HOME/.lumd/priv_validator_state.json.backup $HOME/.lumd/data/priv_validator_state.json
sudo systemctl restart lumd && journalctl -u lumd -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop lumd
cp $HOME/.lumd/data/priv_validator_state.json $HOME/.lumd/priv_validator_state.json.backup
rm -rf $HOME/.lumd/data
curl -o - -L https://lum.snapshot.stavr.tech/lumd/lumd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lumd --strip-components 2
mv $HOME/.lumd/priv_validator_state.json.backup $HOME/.lumd/data/priv_validator_state.json
wget -O $HOME/.lumd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lum/addrbook.json"
sudo systemctl restart lumd && journalctl -u lumd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/LumNetwork-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://lum.api.m.stavr.tech \
🔥RPC🔥:          https://lum.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://lum.grpc.m.stavr.tech:2277 \
🔥peer🔥:         `42d79514ca40e942004e94f90557644cf36e986a@lum.seed.stavr.tech:31316` \
🔥Addrbook🔥:  `wget -O $HOME/.lumd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lum/addrbook.json"` \
🔥Auto_install script🔥:`wget -O lumm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lum/lumm && chmod +x lumm && ./lumm` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Lum/Decentralization)🔥

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

[raw Mainnet json](https://rpc-check.lum.stavr.tech/lum/rpclum_result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>51.15.142.113:26657</td><td>lum-network-1</td><td>sentry-1 🟢</td><td>11422050</td><td>7798847</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T19:35:25.354315924UTC</td></tr><tr><td>176.57.150.227:26657</td><td>lum-network-1</td><td>ELZ-02 🔴</td><td>11422052</td><td>7798847</td><td>False</td><td>off</td><td>4312528</td><td>2024-02-03T19:35:36.110963821UTC</td></tr><tr><td>95.70.184.178:36657</td><td>lum-network-1</td><td>mahof 🔴</td><td>11422055</td><td>7798847</td><td>False</td><td>on</td><td>2661915</td><td>2024-02-03T19:35:55.436349808UTC</td></tr><tr><td>163.172.173.147:26657</td><td>lum-network-1</td><td>sentry-0 🟢</td><td>11422060</td><td>7798847</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T19:36:22.993199979UTC</td></tr><tr><td>51.158.111.136:26657</td><td>lum-network-1</td><td>public-node-0 🟢</td><td>11422061</td><td>7798847</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T19:36:29.861488230UTC</td></tr><tr><td>212.47.250.217:26657</td><td>lum-network-1</td><td>public-node-1 🟢</td><td>11422063</td><td>9165230</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T19:36:38.332498639UTC</td></tr><tr><td>163.172.181.106:26657</td><td>lum-network-1</td><td>lum-validator 🔴</td><td>11422050</td><td>10900615</td><td>False</td><td>on</td><td>169084487</td><td>2024-02-03T19:35:22.993651572UTC</td></tr><tr><td>51.158.102.167:26657</td><td>lum-network-1</td><td>Just-Mining 🔴</td><td>11422055</td><td>11127896</td><td>False</td><td>off</td><td>92295008</td><td>2024-02-03T19:35:52.895268288UTC</td></tr><tr><td>147.135.138.180:26737</td><td>lum-network-1</td><td>CryptoNet 🔴</td><td>11422061</td><td>11317501</td><td>False</td><td>off</td><td>188752</td><td>2024-02-03T19:36:29.519236457UTC</td></tr><tr><td>66.45.246.166:31317</td><td>lum-network-1</td><td>STAVR-Service 🟢</td><td>11422057</td><td>11418501</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T19:36:02.173685999UTC</td></tr></table>
