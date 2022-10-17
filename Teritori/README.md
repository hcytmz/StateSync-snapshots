[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Teritori)
=

# StateSync
```bash
SNAP_RPC="http://88.198.34.226:21097"
peers="3110d11ff2302d4deb6313b4ff5ea982ddeb3ff9@88.198.34.226:21096"
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

# SnapShot 14.10.22 (1 GB) height 163219
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop teritorid
rm -rf $HOME/.teritorid/data/
mkdir $HOME/.teritorid/data/

# download archive
cd $HOME
wget http://teritori.snapshot.stavr.tech:1150/terdata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf terdata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.teritorid/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .teritorid/data/priv_validator_state.json

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm terdata.tar.gz
systemctl restart teritorid && journalctl -u teritorid -f -o cat
```
