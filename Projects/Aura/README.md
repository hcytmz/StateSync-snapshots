<h1 align="center"> 🔥Aura🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Aura)
=
<h1 align="center"> MAINNET</h1>


# State Sync
```python
SNAP_RPC=https://aura.rpc.m.stavr.tech:443
SEEDS="7cefc9a64cd34f6de30e0289d16ee83978f309cc@aura.peers.stavr.tech:21056"
cp $HOME/.aura/data/priv_validator_state.json $HOME/.aura/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.aura/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.aura/config/config.toml
aurad tendermint unsafe-reset-all --home $HOME/.aura --keep-addr-book
mv $HOME/.aura/priv_validator_state.json.backup $HOME/.aura/data/priv_validator_state.json
curl -o - -L http://aura.wasm.stavr.tech:1001/wasm-aura.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2
wget -O $HOME/.aura/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/addrbook.json"
sudo systemctl restart aurad && journalctl -u aurad -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop aurad
cp $HOME/.aura/data/priv_validator_state.json $HOME/.aura/priv_validator_state.json.backup
rm -rf $HOME/.aura/data
curl -o - -L http://aura.snapshot.stavr.tech:5015/aura/aura-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2
curl -o - -L http://aura.wasm.stavr.tech:1102/wasm-aura.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2
mv $HOME/.aura/priv_validator_state.json.backup $HOME/.aura/data/priv_validator_state.json
wget -O $HOME/.aura/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/addrbook.json"
sudo systemctl restart aurad && journalctl -u aurad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Aura-Mainnet/staking        `Indexer "ON"` \
🔥API🔥:          https://aura.api.m.stavr.tech \
🔥RPC🔥:          https://aura.rpc.m.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC🔥:         http://aura.grpc.m.stavr.tech:9901 \
🔥peer🔥:         `7cefc9a64cd34f6de30e0289d16ee83978f309cc@aura.peers.stavr.tech:21056` \
🔥WASM Mainnet🔥:`curl -o - -L http://aura.wasm.stavr.tech:1102/wasm-aura.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.aura --strip-components 2` \
🔥Addrbook🔥:  `wget -O $HOME/.aura/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.aura/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/genesis.json"` \
🔥Auto_install script🔥:`wget -O auram https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Aura/auram && chmod +x auram && ./auram` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Aura/Decentralization)🔥

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

[raw Mainnet json](https://rpc-check.auram.stavr.tech/auram/rpcauram_result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>148.251.88.145:10457</td><td>xstaxy-1</td><td>palamar-archive-node 🟢</td><td>5428277</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:00.989955982UTC</td></tr><tr><td>142.132.202.86:30001</td><td>xstaxy-1</td><td>ramuchi.tech 🟢</td><td>5428279</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:11.134611593UTC</td></tr><tr><td>65.108.141.109:54657</td><td>xstaxy-1</td><td>node 🟢</td><td>5428278</td><td>151001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:03.326841682UTC</td></tr><tr><td>208.77.197.83:27657</td><td>xstaxy-1</td><td>vidulum.app 🟢</td><td>5428274</td><td>3205801</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:40:42.426521112UTC</td></tr><tr><td>144.76.29.90:60757</td><td>xstaxy-1</td><td>UTSA_guide 🟢</td><td>5428279</td><td>4778001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:10.656786398UTC</td></tr><tr><td>5.9.95.147:5857</td><td>xstaxy-1</td><td>Validatrium-rpc 🟢</td><td>5428279</td><td>4967682</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:10.884441656UTC</td></tr><tr><td>65.108.135.212:23357</td><td>xstaxy-1</td><td>2xStake.com 🔴</td><td>5428285</td><td>5055501</td><td>False</td><td>off</td><td>530059</td><td>2024-03-14T04:41:44.988998899UTC</td></tr><tr><td>217.144.98.50:26657</td><td>xstaxy-1</td><td>Noderunners 🔴</td><td>5428279</td><td>5068001</td><td>False</td><td>off</td><td>2026613</td><td>2024-03-14T04:41:10.422700574UTC</td></tr><tr><td>185.246.87.48:21657</td><td>xstaxy-1</td><td>stakrspace 🔴</td><td>5428283</td><td>5122001</td><td>False</td><td>on</td><td>2000310</td><td>2024-03-14T04:41:34.146412777UTC</td></tr><tr><td>65.108.73.245:27657</td><td>xstaxy-1</td><td>tienthuattoan 🟢</td><td>5428284</td><td>5205795</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:38.534079337UTC</td></tr><tr><td>65.109.93.152:34657</td><td>xstaxy-1</td><td>AlxVoy 🟢</td><td>5428279</td><td>5235523</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:10.054780904UTC</td></tr><tr><td>65.108.195.29:51657</td><td>xstaxy-1</td><td>Staketab-snap 🟢</td><td>5428279</td><td>5329201</td><td>False</td><td>off</td><td>0</td><td>2024-03-14T04:41:09.723538308UTC</td></tr><tr><td>135.181.210.171:11047</td><td>xstaxy-1</td><td>STAVR-Service 🟢</td><td>5428283</td><td>5426001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T04:41:33.864044416UTC</td></tr></table>
