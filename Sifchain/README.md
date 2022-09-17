[Node installation instructions](https://github.com/obajay/nodes-Guides/blob/main/Sifchain/README.md)
=

# StateSync
```bash
sudo systemctl stop sifnoded
SNAP_RPC="141.95.124.151:21057"
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

peers="02d427099db530f295efb39e094e23b57132da03@141.95.124.151:21056"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$peers'"|' $HOME/.sifnoded/config/config.toml
sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.sifnoded/config/config.toml
sifnoded tendermint unsafe-reset-all --home $HOME/.sifnoded --keep-addr-book
sudo systemctl restart sifnoded && journalctl -u sifnoded -f -o cat
```
# SnapShot 17.09.22 (0.6 GB) height 8620884
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop sifnoded
rm -rf $HOME/.sifnoded/data/
mkdir $HOME/.sifnoded/data/

# download archive
cd $HOME
wget http://141.95.124.151:5001/sifchaindata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf sifchaindata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.sifnoded/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .sifnoded/data/priv_validator_state.json

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm sifchaindata.tar.gz
systemctl restart sifnoded && journalctl -u sifnoded -f -o cat
```
