[Node installation instructions](https://github.com/obajay/nodes-Guides/blob/main/Sifchain/README.md)
=

# StateSync
```bash
sudo systemctl stop sifnoded
SNAP_RPC="http://sifchain.rpc.m.stavr.tech:13157"
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

peers="cc734391d366c30bf6755dddd07838cfa8731665@135.181.5.47:13156"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$peers'"|' $HOME/.sifnoded/config/config.toml
sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.sifnoded/config/config.toml
sifnoded tendermint unsafe-reset-all --home $HOME/.sifnoded --keep-addr-book
sudo systemctl restart sifnoded && journalctl -u sifnoded -f -o cat
```
# SnapShot (~2.6 GB) updated every 15 hours
```python
cd $HOME
sudo systemctl stop sifnoded
cp $HOME/.sifnoded/data/priv_validator_state.json $HOME/.sifnoded/priv_validator_state.json.backup
rm -rf $HOME/.sifnoded/data
wget http://sifchain.snapshot.stavr.tech:5109/sifchain/sifchain-snap.tar.lz4 && lz4 -c -d $HOME/sifchain-snap.tar.lz4 | tar -x -C $HOME/.sifnoded --strip-components 2
rm -rf sifchain-snap.tar.lz4
mv $HOME/.sifnoded/priv_validator_state.json.backup $HOME/.sifnoded/data/priv_validator_state.json
sudo systemctl restart sifnoded && journalctl -u sifnoded -f -o cat
```
