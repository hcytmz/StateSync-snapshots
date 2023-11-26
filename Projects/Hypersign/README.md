<h1 align="center"> 🔥HyperSign🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Hypersign)
=

<h1 align="center"> TESTNET</h1>

# StateSync HyperSign Testnet
```python
SNAP_RPC=http://hid.rpc.t.stavr.tech:11057
peers="8d558ede2b12c6cbc07d9849accf58cecd521196@hid.peer.stavr.tech:11056"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.hid-node/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.hid-node/config/config.toml
hid-noded tendermint unsafe-reset-all --home $HOME/.hid-node --keep-addr-book
systemctl restart hid-noded && journalctl -u hid-noded -f -o cat
```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop hid-noded
cp $HOME/.hid-node/data/priv_validator_state.json $HOME/.hid-node/priv_validator_state.json.backup
rm -rf $HOME/.hid-node/data
curl -o - -L http://hid.snapshot.stavr.tech:1023/hid/hid-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.hid-node --strip-components 2
mv $HOME/.hid-node/priv_validator_state.json.backup $HOME/.hid-node/data/priv_validator_state.json
wget -O $HOME/.hid-node/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/addrbook.json"
sudo systemctl restart hid-noded && journalctl -u hid-noded -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:      https://explorer.stavr.tech/HyperSign/staking        `Indexer "ON"` \
🔥API:             https://hid.api.t.stavr.tech \
🔥RPC🔥:           http://hid.rpc.t.stavr.tech:11057              `Snapshot-interval = 100` \
🔥gRPC🔥:          http://hid.grpc.t.stavr.tech:8022 \
🔥peer🔥:          `8d558ede2b12c6cbc07d9849accf58cecd521196@hid.peer.stavr.tech:11056` \
🔥Genesis🔥:     ```curl -s  https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/genesis.json > ~/.hid-node/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.hid-node/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O hyper https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/hyper && chmod +x hyper && ./hyper```

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

[raw Testnet json](https://rpc-check.hypert.stavr.tech/hypert/rpc-hypert-result.json)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.69.163:26644</td><td>jagrat</td><td>Brightlystake 🔴</td><td>6292219</td><td>2723801</td><td>False</td><td>173463</td><td>2023-11-25T23:11:13.445458362UTC</td></tr><tr><td>95.217.207.236:24557</td><td>jagrat</td><td>web34ever 🔴</td><td>6292219</td><td>5962514</td><td>False</td><td>223838</td><td>2023-11-25T23:11:16.114128483UTC</td></tr><tr><td>65.109.28.177:29227</td><td>jagrat</td><td>AlxVoy 🔴</td><td>6292219</td><td>6024901</td><td>False</td><td>261966</td><td>2023-11-25T23:11:13.112435288UTC</td></tr><tr><td>23.88.55.152:46657</td><td>jagrat</td><td>cryptobtcbuyer 🔴</td><td>6291992</td><td>6204001</td><td>False</td><td>265132</td><td>2023-11-25T23:11:09.720156642UTC</td></tr><tr><td>213.239.207.175:34657</td><td>jagrat</td><td>landeros 🔴</td><td>6292219</td><td>6229701</td><td>False</td><td>230530</td><td>2023-11-25T23:11:13.704346748UTC</td></tr><tr><td>65.108.238.61:56657</td><td>jagrat</td><td>alex 🟢</td><td>6289493</td><td>6285701</td><td>False</td><td>0</td><td>2023-11-25T23:11:10.048142671UTC</td></tr></table>
