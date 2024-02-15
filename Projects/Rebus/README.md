 <h1 align="center"> 🔥Rebus🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Rebus)
=
# StateSync
```python
SNAP_RPC="https://rebus.rpc.m.stavr.tech:443"
peers="629adb3c3c5331a562a978bc093238ae1b0b6720@rebus.peer.stavr.tech:40106"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.rebusd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.rebusd/config/config.toml
wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"
rebusd tendermint unsafe-reset-all --home ~/.rebusd --keep-addr-book
sudo systemctl restart rebusd && journalctl -u rebusd -f -o cat
```

# SnapShot (~1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop rebusd
cp $HOME/.rebusd/data/priv_validator_state.json $HOME/.rebusd/priv_validator_state.json.backup
rm -rf $HOME/.rebusd/data
curl -o - -L http://rebus.snapshot.stavr.tech:1005/rebus/rebus-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.rebusd --strip-components 2
mv $HOME/.rebusd/priv_validator_state.json.backup $HOME/.rebusd/data/priv_validator_state.json
wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"
sudo systemctl restart rebusd && journalctl -u rebusd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:          https://explorer.stavr.tech/Rebus/staking        Indexer "ON" \
🔥API🔥:                      https://rebus.api.m.stavr.tech \
🔥RPC🔥:                      https://rebus.rpc.m.stavr.tech:443              Snapshot-interval = 300 \
🔥EVM-RPC🔥:                http://rebus.evmrpc.m.stavr.tech:8545 \
🔥gRPC🔥:                    http://rebus.grpc.m.stavr.tech:3211 \
🔥peer🔥:                     `629adb3c3c5331a562a978bc093238ae1b0b6720@rebus.peer.stavr.tech:40106` \
🔥Addrbook🔥:    ```wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O rebuss https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/rebuss && chmod +x rebuss && ./rebuss```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Rebus/Decentralization)🔥
=

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

[raw json Mainnet](https://rpc-check.rebusm.stavr.tech/rebusm/rpc-rebusm-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>83.53.144.71:10657</td><td>reb_1111-1</td><td>Validavia 🔴</td><td>14491177</td><td>8812031</td><td>False</td><td>off</td><td>1029910</td><td>2024-02-15T16:00:32.095598744UTC</td></tr><tr><td>192.99.62.83:26657</td><td>reb_1111-1</td><td>Wefinance-node1 🔴</td><td>14491185</td><td>11258401</td><td>False</td><td>on</td><td>3554001</td><td>2024-02-15T16:00:55.758331894UTC</td></tr><tr><td>89.163.225.99:26657</td><td>reb_1111-1</td><td>mycointainer.com 🔴</td><td>14491174</td><td>12224101</td><td>False</td><td>on</td><td>5731937</td><td>2024-02-15T16:00:18.462441246UTC</td></tr><tr><td>188.165.225.226:26657</td><td>reb_1111-1</td><td>tedcrypto 🔴</td><td>14491182</td><td>12918435</td><td>False</td><td>on</td><td>2203057</td><td>2024-02-15T16:00:45.929526502UTC</td></tr><tr><td>152.53.22.65:26601</td><td>reb_1111-1</td><td>DeFi100-iCosmosDAO 🔴</td><td>14491183</td><td>13173901</td><td>False</td><td>on</td><td>1514008</td><td>2024-02-15T16:00:50.285847129UTC</td></tr><tr><td>54.39.96.230:26657</td><td>reb_1111-1</td><td>api0 🟢</td><td>14491172</td><td>13495101</td><td>False</td><td>on</td><td>0</td><td>2024-02-15T16:00:13.162599882UTC</td></tr><tr><td>65.108.135.212:26652</td><td>reb_1111-1</td><td>2xStake.com 🔴</td><td>14491184</td><td>13664001</td><td>False</td><td>off</td><td>1023471</td><td>2024-02-15T16:00:52.741565004UTC</td></tr><tr><td>149.56.131.26:26657</td><td>reb_1111-1</td><td>api1 🟢</td><td>14491027</td><td>13666501</td><td>False</td><td>on</td><td>0</td><td>2024-02-15T16:00:33.239719511UTC</td></tr><tr><td>65.108.141.109:58657</td><td>reb_1111-1</td><td>node 🟢</td><td>14491174</td><td>14300597</td><td>False</td><td>on</td><td>0</td><td>2024-02-15T16:00:22.983956683UTC</td></tr><tr><td>65.109.65.210:40657</td><td>reb_1111-1</td><td>moodman 🔴</td><td>14491178</td><td>14391178</td><td>False</td><td>off</td><td>1010407</td><td>2024-02-15T16:00:32.508819853UTC</td></tr><tr><td>65.21.170.3:29657</td><td>reb_1111-1</td><td>Munris 🔴</td><td>14491185</td><td>14391184</td><td>False</td><td>off</td><td>1674775</td><td>2024-02-15T16:00:55.140677077UTC</td></tr><tr><td>65.109.35.50:17257</td><td>reb_1111-1</td><td>rebusmos 🟢</td><td>14491174</td><td>14442617</td><td>False</td><td>on</td><td>0</td><td>2024-02-15T16:00:23.378630989UTC</td></tr><tr><td>65.108.66.174:26657</td><td>reb_1111-1</td><td>hello-BccNodesRPC 🟢</td><td>14491174</td><td>14461901</td><td>False</td><td>on</td><td>0</td><td>2024-02-15T16:00:18.126894850UTC</td></tr><tr><td>135.181.210.171:40107</td><td>reb_1111-1</td><td>STAVR-Service 🟢</td><td>14489110</td><td>14488101</td><td>False</td><td>on</td><td>0</td><td>2024-02-15T16:00:15.628500647UTC</td></tr></table>
