[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Agoric)
=
# StateSync Agoric
```bash
SNAP_RPC="51.195.189.48:26657"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash); \

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

peers="e87c695217aa93c3880dd44c97373cdfff5e1226@51.195.189.48:26656"
sed -i -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.agoric/config/config.toml

sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.agoric/config/config.toml
ag0 tendermint unsafe-reset-all --home $HOME/.agoric
sudo systemctl restart agoricd && journalctl -u agoricd -f -o cat
```
