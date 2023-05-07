<h1 align="center"> 🔥Sao Network🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Sao)
=

<h1 align="center"> TESTNET</h1>

# StateSync Sao Testnet (Temporarily stopped)
```python
SNAP_RPC=http://sao.rpc.t.stavr.tech:1077
peers="006e207a3f235a28bc0815001b76ee385ee4bda3@sao.peers.stavr.tech:1076"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.sao/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.sao/config/config.toml
saod tendermint unsafe-reset-all --home /root/.sao --keep-addr-book
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.sao/config/app.toml
sudo systemctl restart saod && journalctl -u saod -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours (Temporarily stopped)
```python
cd $HOME
apt install lz4
sudo systemctl stop saod
cp $HOME/.sao/data/priv_validator_state.json $HOME/.sao/priv_validator_state.json.backup
rm -rf $HOME/.sao/data
curl -o - -L http://sao.snapshot.stavr.tech:1025/sao/sao-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.sao --strip-components 2
mv $HOME/.sao/priv_validator_state.json.backup $HOME/.sao/data/priv_validator_state.json
wget -O $HOME/.sao/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Sao/addrbook.json"
sudo systemctl restart saod && journalctl -u saod -f -o cat
```
