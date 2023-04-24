<h1 align="center"> 🔥HUMANS TESTNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Humans)
=

## StateSync (Temporarily stopped)
```python
SNAP_RPC=http://humans.rpc.t.stavr.tech:1167
peers="7b0b40f045e66d83760859f42e8e95ce7ad93409@humans.peer.stavr.tech:1166"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.humans/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.humans/config/config.toml
humansd tendermint unsafe-reset-all --home $HOME/.humans
wget -O $HOME/.humans/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Humans/addrbook.json"
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.humans/config/app.toml
systemctl restart humansd && journalctl -u humansd -f -o cat

```
## SnapShot (~0.2 GB) updated every 5 hours (Temporarily stopped)
```python
cd $HOME
apt install lz4
sudo systemctl stop humansd
cp $HOME/.humans/data/priv_validator_state.json $HOME/.humans/priv_validator_state.json.backup
rm -rf $HOME/.humans/data
curl -o - -L http://humans.snapshot.stavr.tech:1015/humans/humans-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.humans --strip-components 2
mv $HOME/.humans/priv_validator_state.json.backup $HOME/.humans/data/priv_validator_state.json
wget -O $HOME/.humans/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Humans/addrbook.json"
sudo systemctl restart humansd && journalctl -u humansd -f -o cat
```
