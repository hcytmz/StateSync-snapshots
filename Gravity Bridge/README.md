# StateSync
```bash
SNAP_RPC=141.95.124.151:20757
peers="ff77d192583b59cbdafb47fa12f436efc345506f@141.95.124.151:20756"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.gravity/config/config.toml

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" ~/.gravity/config/config.toml

sudo systemctl stop gravity
gravity tendermint unsafe-reset-all --home $HOME/.gravity

sudo systemctl restart gravity
journalctl -u gravity -f -o cat
```

# Snaphot 15.08.22 (1.3 GB)
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
rm -rf $HOME/.gravity/data/
mkdir $HOME/.gravity/data/

# download archive
cd $HOME
wget http://141.95.124.151:5000/gravitydata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf gravitydata.tar.gz --strip-components 1
# Download addrbook
wget -O $HOME/.gravity/config/addrbook.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Gravity%20Bridge/addrbook.json"
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.gravity/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .gravity/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}

# after unpacking, run the node
sudo systemctl restart gravity
journalctl -u gravity -f -o cat
# don't forget to delete the archive to save space
cd $HOME
rm gravitydata.tar.gz
```
