<h1 align="center"> 🔥Point Netwrok🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Point)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://point.rpc.m.stavr.tech:443
SEEDS=f675d544f5e6b8bc7ef9923d6f594dd0a3570190@point.peer.stavr.tech:1056
cp $HOME/.pointd/data/priv_validator_state.json $HOME/.pointd/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.pointd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.pointd/config/config.toml
pointd tendermint unsafe-reset-all --home $HOME/.pointd --keep-addr-book
mv $HOME/.pointd/priv_validator_state.json.backup $HOME/.pointd/data/priv_validator_state.json
sudo systemctl restart pointd && journalctl -u pointd -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop pointd
cp $HOME/.pointd/data/priv_validator_state.json $HOME/.pointd/priv_validator_state.json.backup
rm -rf $HOME/.pointd/data
curl -o - -L http://point.snapshot.stavr.tech:3/pointd/pointd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.pointd --strip-components 2
mv $HOME/.pointd/priv_validator_state.json.backup $HOME/.pointd/data/priv_validator_state.json
wget -O $HOME/.pointd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Point/addrbook.json"
sudo systemctl restart pointd && journalctl -u pointd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Point-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://point.api.m.stavr.tech \
🔥RPC🔥:          https://point.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://point.grpc.m.stavr.tech:2050 \
🔥peer🔥:         `f675d544f5e6b8bc7ef9923d6f594dd0a3570190@point.peer.stavr.tech:1056` \
🔥Addrbook🔥:  `wget -O $HOME/.pointd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Point/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.pointd/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Point/genesis.json"` \
🔥Auto_install script🔥:`wget -O pointm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Point/pointm && chmod +x pointm && ./pointm`

<details>
<summary>RPC Scanning</summary>

<h2 align="center"> We scan nodes in real time every 4 hours. And we provide the final result of RPC endpoints.
We cannot influence the operation of these nodes in any way. </h2>


```python
If Voting Power is higher than 0 --> then the Node is a validator of the network and may be subject to attack and be a potential threat to the chain.
```
```python
We marked such validators with a red symbol
```

</details>

[raw Mainnet json](https://rpc-check.pointm.stavr.tech/pointm/rpc-pointm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>162.254.36.103:26659</td><td>point_10687-1</td><td>point-mainnet 🟢</td><td>29653357</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-06T09:22:32.109034781UTC</td></tr><tr><td>65.21.90.141:12141</td><td>point_10687-1</td><td>point-mainnet 🔴</td><td>29653354</td><td>29553354</td><td>False</td><td>off</td><td>6501356</td><td>2024-03-06T09:22:27.251100604UTC</td></tr><tr><td>66.45.246.166:1057</td><td>point_10687-1</td><td>STAVR-Service 🟢</td><td>29653358</td><td>29643001</td><td>False</td><td>on</td><td>0</td><td>2024-03-06T09:22:32.643609213UTC</td></tr></table>
