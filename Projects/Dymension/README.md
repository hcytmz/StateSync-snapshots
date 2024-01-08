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
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dymension/Decentralization)🔥


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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>2029435</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:21:31.599344894UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:20:25.200514691UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-01-08T06:21:30.683504242UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>2029425</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:20:28.889689146UTC</td></tr><tr><td>15.235.160.84:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>2029425</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:20:30.756142346UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>2029428</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:20:45.207097522UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>2029428</td><td>1652923</td><td>False</td><td>off</td><td>2</td><td>2024-01-08T06:20:45.847465082UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>2029432</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-08T06:21:12.904904361UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>2029432</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:21:13.349756294UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>2029433</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:18.450720123UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>2029435</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:26.916376707UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>2029436</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-08T06:21:36.510081764UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>2029437</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-08T06:21:42.079707450UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>2029431</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:05.379212882UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>2029435</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:27.322190602UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>2029436</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:36.201333655UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>2029425</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:20:29.181327233UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>2029432</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:13.687426910UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>2029433</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-01-08T06:21:18.188883731UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🔴</td><td>2029436</td><td>1723012</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:36.888748036UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>2029427</td><td>1729427</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:20:40.741776357UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>2029431</td><td>1729430</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:21:02.553919032UTC</td></tr><tr><td>38.242.151.229:33657</td><td>froopyland_100-1</td><td>salomonval 🟢</td><td>2029435</td><td>1773995</td><td>False</td><td>off</td><td>0</td><td>2024-01-08T06:21:27.926220828UTC</td></tr><tr><td>192.99.160.197:26657</td><td>froopyland_100-1</td><td>NodeName 🟢</td><td>1829304</td><td>1826584</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:21:41.827264464UTC</td></tr><tr><td>66.45.236.14:46657</td><td>froopyland_100-1</td><td>Galaxynode 🟢</td><td>2029425</td><td>1938874</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:20:29.793601148UTC</td></tr><tr><td>95.217.222.4:26657</td><td>froopyland_100-1</td><td>STAVR_guide 🔴</td><td>2029435</td><td>1971362</td><td>False</td><td>off</td><td>1</td><td>2024-01-08T06:21:28.346640658UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>2029426</td><td>2007663</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T06:20:35.203250241UTC</td></tr><tr><td>194.233.90.134:26657</td><td>froopyland_100-1</td><td>geonodes 🔴</td><td>2029431</td><td>2015001</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:06.436518798UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>2029424</td><td>2016682</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:20:26.008723610UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>2029431</td><td>2022923</td><td>False</td><td>on</td><td>1</td><td>2024-01-08T06:21:02.919594357UTC</td></tr></table>
