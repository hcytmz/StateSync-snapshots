<h1 align="center"> 🔥CROWD CONTROL TESTNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Crowd%20Control)
=

## StateSync
```python
SNAP_RPC="http://crowd.rpc.t.stavr.tech:21207"
PEERS="0aa2875c176ffda48fe9cd4569d527e629fd868d@crowd.peer.stavr.tech:21206"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.Cardchain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height) \
&& BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)) \
&& TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash); \
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.Cardchain/config/config.toml; \
Cardchaind unsafe-reset-all --home $HOME/.Cardchain
wget -O $HOME/.Cardchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Crowd%20Control/addrbook.json"
sudo systemctl restart Cardchaind && journalctl -u Cardchaind -f -o cat
```
## SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop Cardchaind
cp $HOME/.Cardchain/data/priv_validator_state.json $HOME/.Cardchain/priv_validator_state.json.backup
rm -rf $HOME/.Cardchain/data
curl -o - -L http://crowd.snapshot.stavr.tech:1013/crowd/crowd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.Cardchain --strip-components 2
mv $HOME/.Cardchain/priv_validator_state.json.backup $HOME/.Cardchain/data/priv_validator_state.json
wget -O $HOME/.Cardchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Crowd%20Control/addrbook.json"
sudo systemctl restart Cardchaind && journalctl -u Cardchaind -f -o cat
```
