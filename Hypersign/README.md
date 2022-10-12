[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Hypersign)
=

# StateSync
```bash
SNAP_RPC=http://hid.rpc.t.stavr.tech:21057
peers="2eb8a0e9e8b32e0890a8ecde766e1ab80126fddf@135.181.5.47:21056"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.hid-node/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.hid-node/config/config.toml
hid-noded tendermint unsafe-reset-all --home $HOME/.hid-node
systemctl restart hid-noded && journalctl -u hid-noded -f -o cat
```
# SnapShot 12.10.22 (0.1 GB) height 189856
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop hid-noded
rm -rf $HOME/.hid-node/data/
mkdir $HOME/.hid-node/data/

# download archive
cd $HOME
wget http://hid.snapshot.stavr.tech:7160/hyperdata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf hyperdata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.hid-node/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .hid-node/data/priv_validator_state.json

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm hyperdata.tar.gz
systemctl restart hid-noded && journalctl -u hid-noded -f -o cat
```
