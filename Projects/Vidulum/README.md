<h1 align="center"> 🔥Vidulum🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Vidulum)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://vidulum.rpc.m.stavr.tech:443
SEEDS=197f4d559555de6b7fe360c6a926ca8812a749be@vidulum.peer.stavr.tech:1046
cp $HOME/.vidulum/data/priv_validator_state.json $HOME/.vidulum/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.vidulum/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.vidulum/config/config.toml
vidulumd tendermint unsafe-reset-all --home $HOME/.vidulum --keep-addr-book
mv $HOME/.vidulum/priv_validator_state.json.backup $HOME/.vidulum/data/priv_validator_state.json
sudo systemctl restart vidulumd && journalctl -u vidulumd -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop vidulumd
cp $HOME/.vidulum/data/priv_validator_state.json $HOME/.vidulum/priv_validator_state.json.backup
rm -rf $HOME/.vidulum/data
curl -o - -L https://vidulum.snapshot.stavr.tech/vidulum-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.vidulum --strip-components 2
mv $HOME/.vidulum/priv_validator_state.json.backup $HOME/.vidulum/data/priv_validator_state.json
wget -O $HOME/.vidulum/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Vidulum/addrbook.json"
sudo systemctl restart vidulumd && journalctl -u vidulumd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Vidulum-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://vidulum.api.m.stavr.tech \
🔥RPC🔥:          https://vidulum.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://vidulum.grpc.m.stavr.tech:2040 \
🔥peer🔥:         `197f4d559555de6b7fe360c6a926ca8812a749be@vidulum.peer.stavr.tech:1046` \
🔥Addrbook🔥:  `wget -O $HOME/.vidulum/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Vidulum/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.vidulum/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Vidulum/genesis.json"` \
🔥Auto_install script🔥:`wget -O vdlm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Vidulum/vdlm && chmod +x vdlm && ./vdlm`

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

[raw Mainnet json](https://rpc-check.vidulum.stavr.tech/vidulum/rpc-vidulum-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>208.77.197.82:28657</td><td>vidulum-1</td><td>vidulum.app 🟢</td><td>12840698</td><td>8679101</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T02:49:59.375444088UTC</td></tr><tr><td>185.237.252.152:26652</td><td>vidulum-1</td><td>cryptobtcbuyer 🟢</td><td>12840700</td><td>9758001</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T02:50:14.272338314UTC</td></tr><tr><td>135.181.210.171:1047</td><td>vidulum-1</td><td>STAVR-Service 🟢</td><td>12840699</td><td>12837601</td><td>False</td><td>on</td><td>0</td><td>2024-03-12T02:50:05.773571538UTC</td></tr></table>
