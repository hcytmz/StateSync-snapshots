[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Nois)
=
# StateSync
```bash
SNAP_RPC=http://nois.rpc.t.stavr.tech:21037
peers="2dc7ab934dfec910fac3083fd74e3451e1d3e670@135.181.5.47:21036"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.noisd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.noisd/config/config.toml
noisd tendermint unsafe-reset-all --home $HOME/.noisd --keep-addr-book
systemctl restart noisd && journalctl -u noisd -f -o cat
```

# Snaphot 09.10.22 (0.1 GB) block height --> 46921
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop noisd
rm -rf $HOME/.noisd/data/
mkdir $HOME/.noisd/data/
# download archive
cd $HOME
wget http://nois.snap.stavr.tech:7050/noisddata.tar.gz
# unpack the archive
tar -C $HOME/ -zxvf noisddata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.noisd/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .noisd/data/priv_validator_state.json

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm noisddata.tar.gz
systemctl restart noisd && journalctl -u noisd -f -o cat
```
