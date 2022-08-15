# StateSync Umee
```bash
SNAP_RPC=141.95.124.151:21027
peers="3ac6c5417f461494e9ce778f652922ae59566262@141.95.124.151:21026"
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:21026\"/; s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.umee/config/config.toml

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.umee/config/config.toml
umeed unsafe-reset-all
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
# SnapShot 14.08.22 (29.7 GB)
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
rm -rf $HOME/.umee/data/
mkdir $HOME/.umee/data/

# download archive
cd $HOME
wget http://141.95.124.151:6000/umeedata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf umeedata.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm umeedata.tar.gz
```
