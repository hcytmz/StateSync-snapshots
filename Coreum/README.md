<h1 align="center"> 🔥Coreum🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Althea))
=

<h1 align="center"> TESTNET</h1>

# StateSync Coreum Testnet
```python
SNAP_RPC=http://coreum.rpc.t.stavr.tech:52657
peers=eb5c90c1e845b8a2a989b20fd528097569956ebf@coreum.peer.stavr.tech:17686
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.core/coreum-testnet-1/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.core/coreum-testnet-1/config/config.toml
cored tendermint unsafe-reset-all --home /root/.core/coreum-testnet-1
systemctl restart cored && journalctl -u cored -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop cored
cp $HOME/.core/coreum-testnet-1/data/priv_validator_state.json $HOME/.core/coreum-testnet-1/priv_validator_state.json.backup
rm -rf $HOME/.core/coreum-testnet-1/data
curl -o - -L http://coreum.snapshot.stavr.tech:1022/cored/cored-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.core/coreum-testnet-1 --strip-components 2
mv $HOME/.core/coreum-testnet-1/priv_validator_state.json.backup $HOME/.core/coreum-testnet-1/data/priv_validator_state.json
wget -O $HOME/.core/coreum-testnet-1/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Coreum/addrbook.json"
sudo systemctl restart cored && journalctl -u cored -f -o cat
```
