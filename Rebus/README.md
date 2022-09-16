[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Rebus)
=
# StateSync
```bash
sudo systemctl stop rebusd
peers="9fe60255ffc5176f419d9913ca032d4b5dc413b1@141.95.124.151:20106"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.rebusd/config/config.toml
SNAP_RPC="http://141.95.124.151:20107"
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.rebusd/config/config.toml
wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Rebus/addrbook.json"
rebusd tendermint unsafe-reset-all --home ~/.rebusd --keep-addr-book
sudo systemctl restart rebusd && journalctl -u rebusd -f -o cat
```

=
# SnapShot 16.09.22 (0.3 GB) block height --> 118813
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop rebusd
rm -rf $HOME/.rebusd/data/
mkdir $HOME/.rebusd/data/

# download archive
cd $HOME
wget http://51.195.189.48:7011/rebusdata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf rebusdata.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm rebusdata.tar.gz
# start the node
sudo systemctl restart rebusd && journalctl -u rebusd -f -o cat
```

