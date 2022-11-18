[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Teritori)
=

# StateSync
```bash
SNAP_RPC="http://teritori.rpc.m.stavr.tech:21097"
peers="3110d11ff2302d4deb6313b4ff5ea982ddeb3ff9@teritori.rpc.m.stavr.tech:21096"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.teritorid/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.teritorid/config/config.toml
teritorid tendermint unsafe-reset-all --home $HOME/.teritorid --keep-addr-book
sudo systemctl restart teritorid && journalctl -u teritorid -f -o cat
```

# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
sudo systemctl stop teritorid
cp $HOME/.teritorid/data/priv_validator_state.json $HOME/.teritorid/priv_validator_state.json.backup
rm -rf $HOME/.teritorid/data
wget http://teritori.snapshot.stavr.tech:5000/teritori/teritori-snap.tar.lz4 && lz4 -c -d $HOME/teritori-snap.tar.lz4 | tar -x -C $HOME/.teritorid --strip-components 2
rm -rf teritori-snap.tar.lz4
mv $HOME/.teritorid/priv_validator_state.json.backup $HOME/.teritorid/data/priv_validator_state.json
sudo systemctl restart teritorid && journalctl -u teritorid -f -o cat
```
