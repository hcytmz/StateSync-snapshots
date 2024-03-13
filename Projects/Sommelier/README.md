<h1 align="center"> 🔥Sommelier🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Sommelier)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://somm.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.sommelier/config/config.toml
sommelier tendermint unsafe-reset-all
wget -O $HOME/.sommelier/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Sommelier/addrbook.json"
sudo systemctl restart sommelier && sudo journalctl -u sommelier -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sommelier
cp $HOME/.sommelier/data/priv_validator_state.json $HOME/.sommelier/priv_validator_state.json.backup
rm -rf $HOME/.sommelier/data
curl -o - -L https://sommelier.snapshot.stavr.tech/sommelier/sommelier-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.sommelier --strip-components 2
mv $HOME/.sommelier/priv_validator_state.json.backup $HOME/.sommelier/data/priv_validator_state.json
wget -O $HOME/.sommelier/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Sommelier/addrbook.json"
sudo systemctl restart sommelier && journalctl -u sommelier -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Sommelier-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://som.api.m.stavr.tech \
🔥RPC🔥:          https://somm.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://somm.grpc.m.stavr.tech:114 \
🔥seed🔥:      `ac65237d8760a58be6818566139d33713983d9ef@sommelier.seed.stavr.tech:2076` \
🔥Genesis🔥:   `wget -O $HOME/.sommelier/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Sommelier/genesis.json"` \
🔥Addrbook🔥:  `wget -O $HOME/.sommelier/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Sommelier/addrbook.json"` \
🔥Auto_install script🔥:`wget -O sommm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Sommelier/sommm && chmod +x sommm && ./sommm`

<h1 align="center"> RPC Scanning</h1>

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

[raw Mainnet json](https://rpc-check.somm.stavr.tech/somm/rpc-somm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.181.210.171:2077</td><td>sommelier-3</td><td>STAVR-Service 🟢</td><td>13532907</td><td>12887501</td><td>False</td><td>on</td><td>0</td><td>2024-03-13T11:05:45.172605621UTC</td></tr><tr><td>148.113.6.121:34657</td><td>sommelier-3</td><td>Stakewolle 🔴</td><td>13532916</td><td>13278282</td><td>False</td><td>off</td><td>1121064</td><td>2024-03-13T11:06:36.872515202UTC</td></tr></table>
