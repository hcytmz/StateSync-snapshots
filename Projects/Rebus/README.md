 <h1 align="center"> 🔥Rebus🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Rebus)
=
# StateSync
```python
SNAP_RPC="https://rebus.rpc.m.stavr.tech:443"
peers="629adb3c3c5331a562a978bc093238ae1b0b6720@rebus.peer.stavr.tech:40106"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.rebusd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.rebusd/config/config.toml
wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"
rebusd tendermint unsafe-reset-all --home ~/.rebusd --keep-addr-book
sudo systemctl restart rebusd && journalctl -u rebusd -f -o cat
```

# SnapShot (~1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop rebusd
cp $HOME/.rebusd/data/priv_validator_state.json $HOME/.rebusd/priv_validator_state.json.backup
rm -rf $HOME/.rebusd/data
curl -o - -L http://rebus.snapshot.stavr.tech:1005/rebus/rebus-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.rebusd --strip-components 2
mv $HOME/.rebusd/priv_validator_state.json.backup $HOME/.rebusd/data/priv_validator_state.json
wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"
sudo systemctl restart rebusd && journalctl -u rebusd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:          https://explorer.stavr.tech/Rebus/staking        Indexer "ON" \
🔥API🔥:                      https://rebus.api.m.stavr.tech \
🔥RPC🔥:                      https://rebus.rpc.m.stavr.tech:443              Snapshot-interval = 300 \
🔥EVM-RPC🔥:                http://rebus.evmrpc.m.stavr.tech:7545 \
🔥gRPC🔥:                    http://rebus.grpc.m.stavr.tech:3211 \
🔥peer🔥:                     `629adb3c3c5331a562a978bc093238ae1b0b6720@rebus.peer.stavr.tech:40106` \
🔥Addrbook🔥:    ```wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O rebuss https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/rebuss && chmod +x rebuss && ./rebuss```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Rebus/Decentralization)🔥
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

[raw json Mainnet](https://rpc-check.rebusm.stavr.tech/rebusm/rpc-rebusm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr></table>
