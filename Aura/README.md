[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Aura)
=

# StateSync
```bash
SNAP_RPC="http://aura.rpc.t.stavr.tech:20357"
SEEDS="ca62e050be3c2e688c367e373523ded011dec278@135.181.5.47:20356"
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.aura/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.aura/config/config.toml
aurad tendermint unsafe-reset-all --home $HOME/.aura --keep-addr-book
sudo systemctl restart aurad && journalctl -u aurad -f -o cat
```
# SnapShot 15.11.22 (0.5 GB) height 1886229
```python
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop aura
cp $HOME/.aura/data/priv_validator_state.json $HOME/.aura/priv_validator_state.json.backup
rm -rf $HOME/.aura/data/
mkdir $HOME/.aura/data/

# download archive
cd $HOME
wget http://aura.snapshot.stavr.tech:5000/auradata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf auradata.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm auradata.tar.gz
mv $HOME/.aura/priv_validator_state.json.backup $HOME/.aura/data/priv_validator_state.json
sudo systemctl restart aurad && sudo journalctl -u aurad -f -o cat
```
