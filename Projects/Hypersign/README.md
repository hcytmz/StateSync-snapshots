<h1 align="center"> 🔥HyperSign🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Hypersign)
=

<h1 align="center"> TESTNET</h1>

# StateSync HyperSign Testnet
```python
SNAP_RPC=http://hid.rpc.t.stavr.tech:11057
peers="a3f3d6dba11bfe080693938666064b2324fbaccf@hid.peers.stavr.tech:11056"
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
wget -O $HOME/.hid-node/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Hypersign/addrbook.json"
sudo systemctl restart hid-noded && journalctl -u hid-noded -f -o cat
```
