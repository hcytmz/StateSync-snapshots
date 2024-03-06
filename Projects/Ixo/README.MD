<h1 align="center"> 🔥IXO🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Ixo)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://ixo.rpc.m.stavr.tech:443
SEEDS=d4448c5b10b43d444034533ede7d2e66cbf9e519@ixo.peer.stavr.tech:1016
cp $HOME/.ixod/data/priv_validator_state.json $HOME/.ixod/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.ixod/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.ixod/config/config.toml
ixod tendermint unsafe-reset-all --home $HOME/.ixod --keep-addr-book
mv $HOME/.ixod/priv_validator_state.json.backup $HOME/.ixod/data/priv_validator_state.json
curl -o - -L http://ixo.wasm.stavr.tech:11/wasm-ixod.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ixod --strip-components 2
sudo systemctl restart ixod && journalctl -u ixod -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop ixod
cp $HOME/.ixod/data/priv_validator_state.json $HOME/.ixod/priv_validator_state.json.backup
rm -rf $HOME/.ixod/data
curl -o - -L http://ixo.snapshot.stavr.tech:5/ixod/ixod-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ixod --strip-components 2
curl -o - -L http://ixo.wasm.stavr.tech:11/wasm-ixod.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ixod --strip-components 2
mv $HOME/.ixod/priv_validator_state.json.backup $HOME/.ixod/data/priv_validator_state.json
wget -O $HOME/.ixod/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ixo/addrbook.json"
sudo systemctl restart ixod && journalctl -u ixod -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/IXO-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://ixo.api.m.stavr.tech \
🔥RPC🔥:          https://ixo.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://ixo.grpc.m.stavr.tech:2010 \
🔥peer🔥:         `d4448c5b10b43d444034533ede7d2e66cbf9e519@ixo.peer.stavr.tech:1016` \
🔥Addrbook🔥:  `wget -O $HOME/.ixod/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ixo/addrbook.json"` \
🔥WASM🔥:  `curl -o - -L http://ixo.wasm.stavr.tech:11/wasm-ixod.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ixod --strip-components 2` \
🔥Auto_install script🔥:`wget -O ixom https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ixo/ixom && chmod +x ixom && ./ixom` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Ixo/Decentralization)🔥

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

[raw Mainnet json](https://rpc-check.ixom.stavr.tech/ixom/rpc-ixom-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>62.210.90.254:26657</td><td>ixo-5</td><td>empower-validator 🔴</td><td>5088884</td><td>1</td><td>False</td><td>on</td><td>2214802</td><td>2024-03-06T06:03:05.727244431UTC</td></tr><tr><td>18.166.133.210:26657</td><td>ixo-5</td><td>ixo-hk-sentry-1 🟢</td><td>5088885</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-06T06:03:13.595708047UTC</td></tr><tr><td>66.45.246.166:1017</td><td>ixo-5</td><td>STAVR-Service 🟢</td><td>5088884</td><td>3753001</td><td>False</td><td>on</td><td>0</td><td>2024-03-06T06:03:06.258705085UTC</td></tr></table>
