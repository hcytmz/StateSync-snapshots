<h1 align="center"> 🔥HyperSign🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Hypersign)
=

<h1 align="center"> TESTNET</h1>

# StateSync HyperSign Testnet
```python
SNAP_RPC=https://hid.rpc.t.stavr.tech:443
peers="3845ba311cee9c82469ec2f7b1e5cf8afbd9a434@hid.peer.stavr.tech:11056"
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
🔥RPC🔥:           https://hid.rpc.t.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC🔥:          http://hid.grpc.t.stavr.tech:8022 \
🔥peer🔥:          `3845ba311cee9c82469ec2f7b1e5cf8afbd9a434@hid.peer.stavr.tech:11056` \
🔥Genesis🔥:     ```curl -s  https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/genesis.json > ~/.hid-node/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.hid-node/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O hyper https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Hypersign/hyper && chmod +x hyper && ./hyper``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Hypersign/Decentralization)🔥

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

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>77.83.92.178:26657</td><td>prajna-1</td><td>Sr20de 🔴</td><td>852864</td><td>1</td><td>False</td><td>on</td><td>1080256</td><td>2024-02-14T12:24:04.175832947UTC</td></tr><tr><td>65.109.39.223:26657</td><td>prajna-1</td><td>rjsimp 🔴</td><td>852865</td><td>1</td><td>False</td><td>on</td><td>1187264</td><td>2024-02-14T12:24:08.649094974UTC</td></tr><tr><td>65.108.238.61:56657</td><td>prajna-1</td><td>ams 🔴</td><td>852866</td><td>1</td><td>False</td><td>on</td><td>1226348</td><td>2024-02-14T12:24:15.443946584UTC</td></tr><tr><td>162.55.103.44:26657</td><td>prajna-1</td><td>cwt 🔴</td><td>852867</td><td>1</td><td>False</td><td>on</td><td>989833</td><td>2024-02-14T12:24:18.130519848UTC</td></tr><tr><td>65.109.28.177:29227</td><td>prajna-1</td><td>AlxVoy 🔴</td><td>852867</td><td>1</td><td>False</td><td>on</td><td>1073855</td><td>2024-02-14T12:24:26.937180067UTC</td></tr><tr><td>178.18.254.211:26657</td><td>prajna-1</td><td>CosmoBook 🔴</td><td>852866</td><td>108201</td><td>False</td><td>on</td><td>990495</td><td>2024-02-14T12:24:15.134455593UTC</td></tr><tr><td>23.88.55.152:37657</td><td>prajna-1</td><td>cryptobtcbuyer 🔴</td><td>852867</td><td>752867</td><td>False</td><td>on</td><td>1212386</td><td>2024-02-14T12:24:18.396780170UTC</td></tr><tr><td>135.181.210.171:11057</td><td>prajna-1</td><td>STAVR-Service 🟢</td><td>852866</td><td>849801</td><td>False</td><td>on</td><td>0</td><td>2024-02-14T12:24:15.769178748UTC</td></tr></table>
