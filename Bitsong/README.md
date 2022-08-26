[Node installation instructions](https://github.com/obajay/nodes-Guides/blob/main/Bitsong/README.md)
=
# StateSync
```bash
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
