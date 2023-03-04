[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Nolus)
=

# StateSync
```python
SNAP_RPC=http://nolus.rpc.t.stavr.tech:1177
peers="5bf83be8dfe52fe2c204300f1e9b1449487ce5af@nolus.peer.stavr.tech:1176"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$peers'"|' $HOME/.nolus/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.nolus/config/config.toml
nolusd tendermint unsafe-reset-all --home /root/.nolus --keep-addr-book
systemctl restart nolusd && journalctl -u nolusd -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
rm -rf $HOME/.nolus/data
curl -o - -L http://nolus.snapshot.stavr.tech:1010/nolus/nolus-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.nolus --strip-components 2
curl -o - -L http://nolus.wasm.stavr.tech:1003/wasm-nolus.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.nolus --strip-components 2
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
wget -O $HOME/.nolus/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Nolus/addrbook.json"
sudo systemctl restart nolusd && journalctl -u nolusd -f -o cat
```
