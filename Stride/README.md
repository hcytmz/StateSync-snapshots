[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Stride)
=

# StateSync STRIDE
```python
SNAP_RPC=http://stride.rpc.m.stavr.tech:21017
peers="ce24406f4c7e149e52a75edb8e73dc4501d739b9@stride.rpc.m.stavr.tech:21016"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.stride/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.stride/config/config.toml
strided tendermint unsafe-reset-all --home /root/.stride --keep-addr-book
sudo systemctl restart strided && journalctl -u strided -f -o cat
```
# SnapShot (~0.5GB) updated every 5 hours
```python
cd $HOME
sudo systemctl stop strided
cp $HOME/.stride/data/priv_validator_state.json $HOME/.stride/priv_validator_state.json.backup
rm -rf $HOME/.stride/data
wget http://stride.snapshot.stavr.tech:5011/stride/stride-snap.tar.lz4 && lz4 -c -d $HOME/stride-snap.tar.lz4 | tar -x -C $HOME/.stride --strip-components 2
rm -rf umee-snap.tar.lz4
mv $HOME/.stride/priv_validator_state.json.backup $HOME/.stride/data/priv_validator_state.json
sudo systemctl restart strided && journalctl -u strided -f -o cat
```
