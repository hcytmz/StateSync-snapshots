<h1 align="center"> 🔥Stride🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Stride)
=

# StateSync STRIDE
```python
SNAP_RPC=http://stride.rpc.m.stavr.tech:21017
peers="a7b4cf6f65138ba61518c2c45402da32dc8e28b7@stride.peer.stavr.tech:21016"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.stride/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.stride/config/config.toml
strided tendermint unsafe-reset-all --home /root/.stride --keep-addr-book
sudo systemctl restart strided && journalctl -u strided -f -o cat
```
# SnapShot (~0.8 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop strided
cp $HOME/.stride/data/priv_validator_state.json $HOME/.stride/priv_validator_state.json.backup
rm -rf $HOME/.stride/data
curl -o - -L http://stride.snapshot.stavr.tech:1008/stride/stride-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.stride --strip-components 2
mv $HOME/.stride/priv_validator_state.json.backup $HOME/.stride/data/priv_validator_state.json
wget -O $HOME/.stride/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Stride/addrbook.json"
sudo systemctl restart strided && journalctl -u strided -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:          https://explorer.stavr.tech/stride/staking        Indexer "ON" \
🔥API🔥:                    https://stride.api.m.stavr.tech \
🔥RPC🔥:                      http://stride.rpc.m.stavr.tech:21017              Snapshot-interval = 300 \
🔥gRPC🔥:                    http://stride.grpc.m.stavr.tech:9986 \
🔥peer🔥:                     `a7b4cf6f65138ba61518c2c45402da32dc8e28b7@stride.peer.stavr.tech:21016` \
🔥Addrbook🔥:    ```wget -O $HOME/.stride/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Stride/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O stride-x https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Stride/stride-x && chmod +x stride-x && ./stride-x```
