<h1 align="center"> 🔥Dymension🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

<h1 align="center"> TESTNET</h1>

# StateSync Dymension Testnet
```python
SNAP_RPC=https://dym.rpc.t.stavr.tech:443
peers="263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dymension/config/config.toml
dymd tendermint unsafe-reset-all --home /root/.dymension
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Dymension-testnet/staking        `Indexer "ON"` \
🔥API🔥:          https://dymension.api.t.stavr.tech \
🔥RPC🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis🔥:     ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym```

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

[raw json](https://rpc-check.dymt.stavr.tech/dymt/rpc-dymt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>1378370</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T22:36:51.824799847UTC</td></tr><tr><td>85.190.246.173:33657</td><td>froopyland_100-1</td><td>yatko 🟢</td><td>1378372</td><td>1</td><td>False</td><td>0</td><td>2023-11-22T22:37:01.386610066UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>1378373</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T22:37:06.520054060UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>1378375</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T22:37:18.869033214UTC</td></tr><tr><td>161.97.180.20:26657</td><td>froopyland_100-1</td><td>Blockscope.net 🔴</td><td>1378376</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T22:37:23.880203560UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>1378376</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T22:37:24.263604789UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🟢</td><td>1378376</td><td>1</td><td>False</td><td>0</td><td>2023-11-22T22:37:24.547410569UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>1378370</td><td>106001</td><td>False</td><td>1</td><td>2023-11-22T22:36:52.497523967UTC</td></tr><tr><td>89.116.31.118:26657</td><td>froopyland_100-1</td><td>cardex 🟢</td><td>1378371</td><td>293001</td><td>False</td><td>0</td><td>2023-11-22T22:36:58.951710977UTC</td></tr><tr><td>78.46.103.246:56657</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>1378370</td><td>407001</td><td>False</td><td>1</td><td>2023-11-22T22:36:48.309212416UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>1378374</td><td>591001</td><td>False</td><td>0</td><td>2023-11-22T22:37:10.965899609UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>1378374</td><td>737456</td><td>False</td><td>1</td><td>2023-11-22T22:37:11.349897200UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>1378374</td><td>737456</td><td>False</td><td>1</td><td>2023-11-22T22:37:11.700269678UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>1378368</td><td>820001</td><td>False</td><td>0</td><td>2023-11-22T22:36:40.210031519UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>1378374</td><td>922548</td><td>False</td><td>1</td><td>2023-11-22T22:37:12.008368514UTC</td></tr><tr><td>85.239.240.194:33657</td><td>froopyland_100-1</td><td>zardozmonopoly 🟢</td><td>1378377</td><td>935165</td><td>False</td><td>0</td><td>2023-11-22T22:37:30.493916773UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>1378375</td><td>1006001</td><td>False</td><td>1</td><td>2023-11-22T22:37:18.487908346UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>1378372</td><td>1078372</td><td>False</td><td>0</td><td>2023-11-22T22:37:03.716554620UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>1378376</td><td>1150548</td><td>False</td><td>1</td><td>2023-11-22T22:37:26.852501587UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>1378370</td><td>1158907</td><td>False</td><td>1</td><td>2023-11-22T22:36:49.409546157UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1378367</td><td>1238063</td><td>False</td><td>0</td><td>2023-11-22T22:36:35.223205543UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1378375</td><td>1318001</td><td>False</td><td>0</td><td>2023-11-22T22:37:21.263081483UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>1378368</td><td>1330001</td><td>False</td><td>1</td><td>2023-11-22T22:36:40.539356601UTC</td></tr><tr><td>20.122.112.2:36657</td><td>froopyland_100-1</td><td>dymdtestnet 🟢</td><td>1378369</td><td>1368573</td><td>False</td><td>0</td><td>2023-11-22T22:36:43.384906737UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>1378372</td><td>1370001</td><td>False</td><td>1</td><td>2023-11-22T22:37:04.112303637UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>1378369</td><td>1375975</td><td>False</td><td>0</td><td>2023-11-22T22:36:43.855107837UTC</td></tr></table>
