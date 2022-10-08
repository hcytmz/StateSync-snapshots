[Node installation instructions](https://github.com/obajay/nodes-Guides/blob/main/Bitcanna/README.md)
=

# StateSync
```bash
RPC="http://bitcanna.rpc.m.stavr.tech:21327"
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

peers="f5ab20ff53ddaa2a473c23694b4bac2c187d7b2a@135.181.5.47:21326"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.bcna/config/config.toml
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.bcna/config/config.toml
sudo systemctl stop bcnad && bcnad tendermint unsafe-reset-all --keep-addr-book
sudo systemctl restart bcnad && sudo journalctl -u bcnad -f -o cat
```
# SnapShot 08.10.22 (0.2 GB) height 5346921
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop bcnad
rm -rf $HOME/.bcna/data/
mkdir $HOME/.bcna/data/

# download archive
cd $HOME
wget http://bitcanna.snapshot.stavr.tech:5101/bitcannaindata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf bitcannaindata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.bcna/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .bcna/data/priv_validator_state.json

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
wget -O $HOME/.bcna/config/genesis.json "https://raw.githubusercontent.com/BitCannaGlobal/bcna/main/genesis.json"
rm bitcannaindata.tar.gz
sudo systemctl restart bcnad && sudo journalctl -u bcnad -f -o cat
```
