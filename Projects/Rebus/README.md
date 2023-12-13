 <h1 align="center"> 🔥Rebus🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Rebus)
=
# StateSync
```python
SNAP_RPC="http://rebus.rpc.m.stavr.tech:40107"
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
🔥RPC🔥:                      http://rebus.rpc.m.stavr.tech:40107              Snapshot-interval = 300 \
🔥EVM-RPC🔥:                http://rebus.evmrpc.m.stavr.tech:8545 \
🔥gRPC🔥:                    http://rebus.grpc.m.stavr.tech:3211 \
🔥peer🔥:                     `629adb3c3c5331a562a978bc093238ae1b0b6720@rebus.peer.stavr.tech:40106` \
🔥Addrbook🔥:    ```wget -O $HOME/.rebusd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O rebuss https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Rebus/rebuss && chmod +x rebuss && ./rebuss```

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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>141.94.141.144:34457</td><td>reb_1111-1</td><td>cyberG 🔴</td><td>12663774</td><td>8486101</td><td>False</td><td>on</td><td>1045626</td><td>2023-12-13T02:19:36.127203013UTC</td></tr><tr><td>83.53.145.221:10657</td><td>reb_1111-1</td><td>Validavia 🔴</td><td>12663772</td><td>8812031</td><td>False</td><td>off</td><td>1027814</td><td>2023-12-13T02:19:30.755530246UTC</td></tr><tr><td>65.108.226.26:18657</td><td>reb_1111-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>12663779</td><td>9280501</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:19:48.849171560UTC</td></tr><tr><td>188.165.225.226:26657</td><td>reb_1111-1</td><td>tedcrypto 🔴</td><td>12663770</td><td>10217701</td><td>False</td><td>on</td><td>2148824</td><td>2023-12-13T02:19:23.709442159UTC</td></tr><tr><td>65.109.35.50:17257</td><td>reb_1111-1</td><td>rebusmos 🟢</td><td>12663763</td><td>10844401</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:19:03.893717850UTC</td></tr><tr><td>65.108.135.212:26652</td><td>reb_1111-1</td><td>2xStake.com 🔴</td><td>12663772</td><td>11112501</td><td>False</td><td>off</td><td>1067501</td><td>2023-12-13T02:19:30.285649759UTC</td></tr><tr><td>65.108.141.109:58657</td><td>reb_1111-1</td><td>node 🟢</td><td>12663763</td><td>11172401</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:19:03.577553572UTC</td></tr><tr><td>192.99.62.83:26657</td><td>reb_1111-1</td><td>Wefinance-node1 🔴</td><td>12663774</td><td>11258401</td><td>False</td><td>on</td><td>3357505</td><td>2023-12-13T02:19:35.828636912UTC</td></tr><tr><td>65.108.66.174:26657</td><td>reb_1111-1</td><td>hello-BccNodesRPC 🟢</td><td>12663762</td><td>12105701</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:18:58.643480875UTC</td></tr><tr><td>89.163.225.99:26657</td><td>reb_1111-1</td><td>mycointainer.com 🔴</td><td>12663762</td><td>12224101</td><td>False</td><td>on</td><td>4975337</td><td>2023-12-13T02:18:58.987037686UTC</td></tr><tr><td>54.39.96.230:26657</td><td>reb_1111-1</td><td>api0 🟢</td><td>12663761</td><td>12372001</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:18:55.830809400UTC</td></tr><tr><td>149.56.131.26:26657</td><td>reb_1111-1</td><td>api1 🟢</td><td>12663765</td><td>12529901</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:19:11.169595580UTC</td></tr><tr><td>65.109.65.210:40657</td><td>reb_1111-1</td><td>moodman 🔴</td><td>12663765</td><td>12563765</td><td>False</td><td>off</td><td>1097991</td><td>2023-12-13T02:19:10.461199833UTC</td></tr><tr><td>65.21.170.3:29657</td><td>reb_1111-1</td><td>Munris 🔴</td><td>12663773</td><td>12563773</td><td>False</td><td>off</td><td>1497155</td><td>2023-12-13T02:19:33.156041927UTC</td></tr><tr><td>135.181.210.171:40107</td><td>reb_1111-1</td><td>STAVR-Service 🟢</td><td>12659910</td><td>12659301</td><td>False</td><td>on</td><td>0</td><td>2023-12-13T02:18:56.214184683UTC</td></tr></table>