<h1 align="center"> 🔥Uptick🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Uptick)
=

<h1 align="center"> MAINNET</h1>

# StateSync Uptick Mainnet
```python
SNAP_RPC=http://uptick.rpc.m.stavr.tech:3157
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.uptickd/config/config.toml
uptickd tendermint unsafe-reset-all --home $HOME/.uptickd
wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/addrbook.json"
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.uptickd/config/app.toml
sudo systemctl restart uptickd && journalctl -u uptickd -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop uptickd
cp $HOME/.uptickd/data/priv_validator_state.json $HOME/.uptickd/priv_validator_state.json.backup
rm -rf $HOME/.uptickd/data
curl -o - -L http://uptick.snapshot.stavr.tech:1027/uptickd/uptickd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.uptickd --strip-components 2
mv $HOME/.uptickd/priv_validator_state.json.backup $HOME/.uptickd/data/priv_validator_state.json
wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/addrbook.json"
sudo systemctl restart uptickd && journalctl -u uptickd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:         https://explorer.stavr.tech/Uptick-Mainnet      `Indexer "ON"` \
🔥EXPLORER Testnet🔥:           https://explorer.stavr.tech/uptick/staking        `Indexer "ON"` \
🔥API Mainnet🔥:                      https://uptick.api.m.stavr.tech \
🔥API Testnet🔥:                        https://uptick.api.t.stavr.tech \
🔥RPC🔥:                                      http://uptick.rpc.m.stavr.tech:3157              `Snapshot-interval = 100` \
🔥gRPC🔥:                                    http://uptick.grpc.m.stavr.tech:1901 \
🔥peer🔥:                                    `ee147b5a411750138a7add20dd004e4f8f1a2179@uptick.peers.stavr.tech:3156` \
🔥Genesis🔥:    ```wget -O $HOME/.uptickd/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/genesis.json"``` \
🔥Addrbook🔥:    ```wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O uptickm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Uptick/uptickm && chmod +x uptickm && ./uptickm```
