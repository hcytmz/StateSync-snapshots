<h1 align="center"> 🔥JACKAL🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Jakal)
=

<h1 align="center"> MAINNET</h1>

# StateSync Jackal Mainnet
```python
SNAP_RPC=http://jkl.rpc.m.stavr.tech:11127
peers="26b6255375a592c3b0664bd474a6975f468c3785@jkl.rpc.m.stavr.tech:11126"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.canine/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
canined tendermint unsafe-reset-all --home /root/.canine --keep-addr-book
systemctl restart canined && journalctl -u canined -f -o cat
```
# SnapShot (~1.2GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop canined
cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup
rm -rf $HOME/.canine/data
curl -o - -L http://jkl.snapshot.stavr.tech:1006/jackal/jackal-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.canine --strip-components 2
mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json
wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"
sudo systemctl restart canined && journalctl -u canined -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Jakal/Jackal-Testnet)
=

# StateSync Jackal Testnet
```python
SNAP_RPC=http://jkl.rpc.t.stavr.tech:19127
peers="8a11570dbaa0f4d98ca2ef0ad117e9c1154d81b9@jkltest.peer.stavr.tech:19126"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.canine/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
canined tendermint unsafe-reset-all --home /root/.canine --keep-addr-book
systemctl restart canined && journalctl -u canined -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop canined
cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup
rm -rf $HOME/.canine/data
curl -o - -L http://jkltest.snapshot.stavr.tech:1015/jackalt/jackalt-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.canine --strip-components 2
mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json
wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"
sudo systemctl restart canined && journalctl -u canined -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Jackal/staking		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Jackal-Testnet/staking     `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://jkl.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://jkl.api.t.stavr.tech \
🔥RPC Mainnet🔥:           http://jkl.rpc.m.stavr.tech:11127              `Snapshot-interval = 300` \
🔥RPC Testnet🔥:           http://jkl.rpc.t.stavr.tech:19127              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:          http://jkl.grpc.m.stavr.tech:5013 \
🔥gRPC Testnet🔥:          http://jkl.grpc.t.stavr.tech:5913 \
🔥peer Mainnet🔥:					 `26b6255375a592c3b0664bd474a6975f468c3785@jkl.peer.stavr.tech:11126` \
🔥peer Testnet🔥:					 `8a11570dbaa0f4d98ca2ef0ad117e9c1154d81b9@jkltest.peer.stavr.tech:19126` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O jkl https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/jkl && chmod +x jkl && ./jkl``` \
🔥Auto_install script Testnet🔥: ```wget -O jkltest https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/jkltest && chmod +x jkltest && ./jkltest```
