
<h1 align="center"> 🔥Empower🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Empower)
=

<h1 align="center"> MAINNET</h1>

# StateSync Mainnet
```python
SNAP_RPC=https://empw.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.empowerchain/config/config.toml
empowerd tendermint unsafe-reset-all --home $HOME/.empowerchain
curl -o - -L https://empw.wasm.stavr.tech/wasm-empw.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2
wget -O $HOME/.empowerchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/addrbook.json"
systemctl restart empowerd && journalctl -u empowerd -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop empowerd
cp $HOME/.empowerchain/data/priv_validator_state.json $HOME/.empowerchain/priv_validator_state.json.backup
rm -rf $HOME/.empowerchain/data
curl -o - -L https://empw-m.snapshot.stavr.tech/empw-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2
curl -o - -L https://empw.wasm.stavr.tech/wasm-empw.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2
mv $HOME/.empowerchain/priv_validator_state.json.backup $HOME/.empowerchain/data/priv_validator_state.json
wget -O $HOME/.empowerchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/addrbook.json"
sudo systemctl restart empowerd && sudo journalctl -u empowerd -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Empower/Testnet)
=


# StateSync Testnet
```python
SNAP_RPC=http://empw.rpc.t.stavr.tech:22057
peers="a8f7749ee8ba55b5c2181a1591d7e291db594883@empw.peers.stavr.tech:22056"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.empowerchain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.empowerchain/config/config.toml
empowerd tendermint unsafe-reset-all --home $HOME/.empowerchain
wget -O $HOME/.empowerchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/Testnet/addrbook.json"
curl -o - -L http://empw.wasm.stavr.tech:1001/wasm-empw.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2
systemctl restart empowerd && journalctl -u empowerd -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop empowerd
cp $HOME/.empowerchain/data/priv_validator_state.json $HOME/.empowerchain/priv_validator_state.json.backup
rm -rf $HOME/.empowerchain/data
curl -o - -L http://empw.snapshot.stavr.tech:1031/empw/empw-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2
curl -o - -L http://empw.wasm.stavr.tech:1001/wasm-empw.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2
mv $HOME/.empowerchain/priv_validator_state.json.backup $HOME/.empowerchain/data/priv_validator_state.json
wget -O $HOME/.empowerchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/Testnet/addrbook.json"
sudo systemctl restart empowerd && sudo journalctl -u empowerd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER M🔥:          https://explorer.stavr.tech/Empower-Mainnet        `Indexer "ON"` \
🔥EXPLORER T🔥:          https://explorer.stavr.tech/Empower        `Indexer "ON"` \
🔥API M🔥:                       https://empw.api.m.stavr.tech \
🔥API T🔥:                       https://empw.api.t.stavr.tech \
🔥RPC M🔥:                      https://empw.rpc.m.stavr.tech:443              `Snapshot-interval = 500`  \
🔥RPC T🔥:                      http://empw.rpc.t.stavr.tech:22057              `Snapshot-interval = 100` \
🔥gRPC M🔥:                    http://empw.grpc.m.stavr.tech:9141 \
🔥gRPC T🔥:                    http://empw.grpc.t.stavr.tech:9141 \
🔥peer M🔥:                     `192d6c396fe0f9da1b1b700aab8bdd1ce6a49490@empw-m.peers.stavr.tech:22056` \
🔥peer T🔥:                     `a8f7749ee8ba55b5c2181a1591d7e291db594883@empw.peers.stavr.tech:22056` \
🔥WASM T🔥:```curl -o - -L http://empw.wasm.stavr.tech:1001/wasm-empw.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.empowerchain --strip-components 2``` \
🔥Addrbook M🔥:    ```wget -O $HOME/.empowerchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/addrbook.json"``` \
🔥Addrbook T🔥:    ```wget -O $HOME/.empowerchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/Testnet/addrbook.json"``` \
🔥Genesis🔥:     ```wget -O $HOME/.empowerchain/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/Testnet/genesis.json"``` \
🔥Auto_install script🔥M: ```wget -O empwm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/empwm && chmod +x empwm && ./empwm``` \
🔥Auto_install script🔥T: ```wget -O empw https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Empower/Testnet/empw && chmod +x empw && ./empw```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Empower/Decentralization)🔥
=

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

[raw json](https://rpc-check.empwm.stavr.tech/empwm/rpc-empwm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.181.58.28:22357</td><td>empowerchain-1</td><td>Validatrium-rpc 🟢</td><td>3909742</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:10:25.867343880UTC</td></tr><tr><td>62.210.173.13:26657</td><td>empowerchain-1</td><td>node 🟢</td><td>3909743</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:10:32.484682377UTC</td></tr><tr><td>93.115.25.178:4002</td><td>empowerchain-1</td><td>Zenscape 🟢</td><td>3909749</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:11:06.788778893UTC</td></tr><tr><td>83.53.145.231:17657</td><td>empowerchain-1</td><td>Validavia 🔴</td><td>3909748</td><td>263410</td><td>False</td><td>off</td><td>18502</td><td>2024-03-07T20:11:04.100985486UTC</td></tr><tr><td>161.97.82.203:31657</td><td>empowerchain-1</td><td>ams-rpc 🟢</td><td>3909742</td><td>2608201</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:10:25.565903943UTC</td></tr><tr><td>142.132.157.153:17457</td><td>empowerchain-1</td><td>yldmsempower 🟢</td><td>3848179</td><td>2700001</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:10:26.100545692UTC</td></tr><tr><td>74.208.94.42:26848</td><td>empowerchain-1</td><td>39937AF 🟢</td><td>3909746</td><td>3798001</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:10:51.499120976UTC</td></tr><tr><td>65.108.230.113:22057</td><td>empowerchain-1</td><td>STAVR-Service 🟢</td><td>3909748</td><td>3909001</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T20:11:04.422145440UTC</td></tr></table>
