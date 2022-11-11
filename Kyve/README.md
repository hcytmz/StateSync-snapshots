[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Kyve)
=
# State Sync KYVE (korellia)
```bash
SNAP_RPC1="141.95.124.151:20057" \
&& SNAP_RPC2="65.108.126.46:28657" \
&& SNAP_RPC3="65.108.57.92:26657" \
&& SNAP_RPC4="95.216.157.18:26657"
peers="e9a2567ee5fda3f98fce7b0e4342ef1e85c9fed9@141.95.124.151:20056,287c511b6ca0c6a5853cf52021bbbabfee6c7219@65.108.126.46:28656,d040c94305f0b421df815d5375201b34f8cae999@65.108.57.92:26656,2823ef5801b138802d076bf3e0478ec9be4e7bde@95.216.157.18:26656"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.kyve/config/config.toml

LATEST_HEIGHT=$(curl -s $SNAP_RPC1/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC1/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC1,$SNAP_RPC2,$SNAP_RPC3,$SNAP_RPC4\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.kyve/config/config.toml
chaind tendermint unsafe-reset-all --home $HOME/.kyve
chaind tendermint unsafe-reset-all --home $HOME/.kyve
sudo systemctl restart kyved && journalctl -u kyved -f -o cat
```
[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Kyve/beta)
=
# State Sync KYVE (kyve-beta)
```bash
SNAP_RPC="kyveb.rpc.t.stavr.tech:20057"
peers="4d7740c5ba34ade97bb6491422eab414b7831ca0@135.181.5.47:20056"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.kyve/config/config.toml

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.kyve/config/config.toml
chaind tendermint unsafe-reset-all --home $HOME/.kyve
sudo systemctl restart kyved && journalctl -u kyved -f -o cat
```
# SnapShot KYVE-BETA 11.11.22 (0.1 GB) height 919269
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop chaind
cp $HOME/.kyve/data/priv_validator_state.json $HOME/.kyve/priv_validator_state.json.backup
rm -rf $HOME/.kyve/data/
mkdir $HOME/.kyve/data/

# download archive
cd $HOME
wget http://kyvebeta.snapshot.stavr.tech:5102/kyvedata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf kyvedata.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm kyvedata.tar.gz
wget -O $HOME/.kyve/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Kyve/beta/addrbook.json"
mv $HOME/.kyve/priv_validator_state.json.backup $HOME/.kyve/data/priv_validator_state.json
sudo systemctl restart chaind && sudo journalctl -u chaind -f -o cat
```
