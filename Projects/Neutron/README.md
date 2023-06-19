<h1 align="center"> 🔥Neutron🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Neutron)
=
# StateSync   (Temporarily stopped)
```python
SNAP_RPC=http://neutron.rpc.t.stavr.tech:11057
peers="b81828b92f6e58eaa211fbb21c08cf809cdefa94@neutron.rpc.t.stavr.tech:11056"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.neutrond/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.neutrond/config/config.toml
neutrond tendermint unsafe-reset-all --home /root/.neutrond --keep-addr-book
```
# SnapShot (0.1 GB)    (Temporarily stopped)
```python
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop neutrond
cp $HOME/.neutrond/data/priv_validator_state.json $HOME/.neutrond/priv_validator_state.json.backup
rm -rf $HOME/.neutrond/data/
mkdir $HOME/.neutrond/data/

# download archive
cd $HOME
wget http://neutron.snapshot.stavr.tech:4000/neutronddata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf neutronddata.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm neutronddata.tar.gz
mv $HOME/.neutrond/priv_validator_state.json.backup $HOME/.neutrond/data/priv_validator_state.json
sudo systemctl restart neutrond && sudo journalctl -u neutrond -f -o cat
```
