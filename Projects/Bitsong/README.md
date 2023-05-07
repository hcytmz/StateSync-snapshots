<h1 align="center"> 🔥Bitsong🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/blob/main/Bitsong/README.md)
=
# StateSync
```python
RPC="51.195.189.48:21037"
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

peers="eddccf92e8d7d746f6a42ad08b9800037e3633cf@51.195.189.48:21036"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.bitsongd/config/config.toml

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.bitsongd/config/config.toml
bitsongd tendermint unsafe-reset-all --home /root/.bitsongd
wget -O $HOME/.bitsongd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Bitsong/addrbook.json"
sudo systemctl restart bitsongd && journalctl -u bitsongd -f -o cat
```

# Snaphot  (0.8 GB) 
```python
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop bitsongd
rm -rf $HOME/.bitsongd/data/
mkdir $HOME/.bitsongd/data/
# download archive
cd $HOME
wget http://51.195.189.48:7000/bitsongddata.tar.gz
# unpack the archive
tar -C $HOME/ -zxvf bitsongddata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.bitsongd/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .bitsongd/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}
# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm bitsongddata.tar.gz
sudo systemctl restart bitsongd && sudo journalctl -u bitsongd -f -o cat
```
