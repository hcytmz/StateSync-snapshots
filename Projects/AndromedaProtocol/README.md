<h1 align="center"> 🔥AndromedaProtocol🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/AndromedaProtocol)
=

<h1 align="center"> TESTNET</h1>

# StateSync Andromedad Testnet
```python
SNAP_RPC=http://andromedad.rpc.t.stavr.tech:4137
peers="d083506ef2e9d5f2ee22dabf4fa893a72e6cf483@andromedad.peer.stavr.tech:4376"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.andromedad/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.andromedad/config/config.toml
andromedad tendermint unsafe-reset-all --home $HOME/.andromedad
systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop andromedad
cp $HOME/.andromedad/data/priv_validator_state.json $HOME/.andromedad/priv_validator_state.json.backup
rm -rf $HOME/.andromedad/data
curl -o - -L http://andromedad.snapshot.stavr.tech:1021/andromedad/andromedad-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2
curl -o - -L http://andromedad.wasm.stavr.tech:1002/wasm-andromedad.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2
mv $HOME/.andromedad/priv_validator_state.json.backup $HOME/.andromedad/data/priv_validator_state.json
wget -O $HOME/.andromedad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"
sudo systemctl restart andromedad && journalctl -u andromedad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:    https://explorer.stavr.tech/Andromedad-testnet/staking            `Indexer "ON"` \
🔥API🔥:         https://andromedad.api.t.stavr.tech \
🔥RPC🔥:         http://andromedad.rpc.t.stavr.tech:4137                  `Snapshot-interval = 100` \
🔥gRPC🔥:        http://andromedad.grpc.t.stavr.tech:11090 \
🔥peer🔥:        `d083506ef2e9d5f2ee22dabf4fa893a72e6cf483@andromedad.peer.stavr.tech:4376` \
🔥WASM🔥: updated every 10 hours `curl -o - -L http://andromedad.wasm.stavr.tech:1002/wasm-andromedad.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.andromedad --strip-components 2` \
🔥Genesis🔥: `wget -O $HOME/.andromedad/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/genesis.json"` \
🔥Addrbook🔥: `wget -O $HOME/.andromedad/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/addrbook.json"` \
🔥Auto_install script🔥: `wget -O adprotocol https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/AndromedaProtocol/adprotocol && chmod +x adprotocol && ./adprotocol`


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.93.35:50657</td><td>galileo-3</td><td>Synergy_Nodes 🟢</td><td>3920371</td><td>0</td><td>False</td><td>0</td><td>2023-11-22T08:14:58.091900915UTC</td></tr><tr><td>65.108.199.120:61357</td><td>galileo-3</td><td>RAMZES 🟢</td><td>3920367</td><td>1</td><td>False</td><td>0</td><td>2023-11-22T08:14:37.519082182UTC</td></tr><tr><td>142.132.209.236:21257</td><td>galileo-3</td><td>a4951031-6d09-5ee9-9e28-e063741b480d 🔴</td><td>3920370</td><td>1</td><td>False</td><td>3</td><td>2023-11-22T08:14:52.936810223UTC</td></tr><tr><td>65.21.133.114:56657</td><td>galileo-3</td><td>Staketab 🔴</td><td>3920371</td><td>90001</td><td>False</td><td>2</td><td>2023-11-22T08:14:59.056407401UTC</td></tr><tr><td>65.109.70.45:15657</td><td>galileo-3</td><td>L0vd.com 🔴</td><td>3920371</td><td>659001</td><td>False</td><td>3</td><td>2023-11-22T08:14:57.747566814UTC</td></tr><tr><td>65.109.116.119:14757</td><td>galileo-3</td><td>semalist 🔴</td><td>3920366</td><td>2228721</td><td>False</td><td>1318</td><td>2023-11-22T08:14:30.018538618UTC</td></tr><tr><td>213.239.207.175:42657</td><td>galileo-3</td><td>landeros 🔴</td><td>3920364</td><td>2642001</td><td>False</td><td>72</td><td>2023-11-22T08:14:18.578765100UTC</td></tr><tr><td>161.97.152.157:27657</td><td>galileo-3</td><td>cardex 🟢</td><td>3920371</td><td>2945323</td><td>False</td><td>0</td><td>2023-11-22T08:14:58.698748936UTC</td></tr><tr><td>65.109.88.254:40657</td><td>galileo-3</td><td>ksalab 🔴</td><td>3920366</td><td>3000356</td><td>False</td><td>31919</td><td>2023-11-22T08:14:31.031577116UTC</td></tr><tr><td>78.46.103.246:60957</td><td>galileo-3</td><td>F5Nodes 🔴</td><td>3920371</td><td>3057001</td><td>False</td><td>24</td><td>2023-11-22T08:14:58.358970212UTC</td></tr><tr><td>65.108.227.112:14657</td><td>galileo-3</td><td>[NODERS]TEAM 🔴</td><td>3920364</td><td>3176323</td><td>False</td><td>959616</td><td>2023-11-22T08:14:18.909813543UTC</td></tr><tr><td>138.201.53.44:33657</td><td>galileo-3</td><td>EdWWWardo 🟢</td><td>3920137</td><td>3406335</td><td>False</td><td>0</td><td>2023-11-22T08:14:23.280791028UTC</td></tr><tr><td>194.34.232.224:56657</td><td>galileo-3</td><td>andromeda 🟢</td><td>3920366</td><td>3820366</td><td>False</td><td>0</td><td>2023-11-22T08:14:30.361105362UTC</td></tr><tr><td>65.21.170.3:32657</td><td>galileo-3</td><td>Munris 🔴</td><td>3920369</td><td>3820369</td><td>False</td><td>411</td><td>2023-11-22T08:14:46.536744628UTC</td></tr><tr><td>95.217.108.25:36657</td><td>galileo-3</td><td>tRDM 🔴</td><td>3920370</td><td>3914001</td><td>False</td><td>75</td><td>2023-11-22T08:14:55.306973068UTC</td></tr><tr><td>194.163.174.231:26677</td><td>galileo-3</td><td>AviaDoc_by_AviaOne 🟢</td><td>3920369</td><td>3915001</td><td>False</td><td>0</td><td>2023-11-22T08:14:46.110231160UTC</td></tr><tr><td>135.181.210.171:4137</td><td>galileo-3</td><td>STAVR-Service 🟢</td><td>3920366</td><td>3919201</td><td>False</td><td>0</td><td>2023-11-22T08:14:30.694892168UTC</td></tr></table>