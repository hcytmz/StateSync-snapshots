<h1 align="center"> 🔥C4E🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/C4E)
=

<h1 align="center"> MAINNET</h1>

# StateSync C4E Mainnet
```python
SNAP_RPC=http://c4e.rpc.m.stavr.tech:17097
peers="5ed0b8f7989d34438f71ccc74b0ab0fbf763a475@c4e.peer.stavr.tech:17096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.c4e-chain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.c4e-chain/config/config.toml
c4ed tendermint unsafe-reset-all --home /root/.c4e-chain --keep-addr-book
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop c4ed
cp $HOME/.c4e-chain/data/priv_validator_state.json $HOME/.c4e-chain/priv_validator_state.json.backup
rm -rf $HOME/.c4e-chain/data
curl -o - -L http://c4e.snapshot.stavr.tech:1018/c4e/c4e-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.c4e-chain --strip-components 2
mv $HOME/.c4e-chain/priv_validator_state.json.backup $HOME/.c4e-chain/data/priv_validator_state.json
wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/addrbook.json"
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER MAINNET🔥:  https://explorer.stavr.tech/C4E/staking            `Indexer "ON"` \
🔥EXPLORER TESTET🔥:   https://explorer.stavr.tech/C4E-Testnet/staking     `Indexer "ON"` \
🔥API MAINNET🔥:       https://c4e.api.m.stavr.tech \
🔥API TESTNET🔥:       https://c4e.api.t.stavr.tech \
🔥RPC🔥:               http://c4e.rpc.m.stavr.tech:17097                  `Snapshot-interval = 100` \
🔥gRPC🔥:              http://c4e.grpc.m.stavr.tech:7029 \
🔥peer🔥:              `5ed0b8f7989d34438f71ccc74b0ab0fbf763a475@c4e.peer.stavr.tech:17096` \
🔥Addrbook🔥:    ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/genesis.json -O $HOME/.c4e-chain/config/genesis.json``` \
🔥Auto_install script🔥: ```wget -O c4 https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/c4 && chmod +x c4 && ./c4```





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

[raw json](https://rpc-check.c4e.stavr.tech/c4e/rpc-c4e-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.21.129.95:36657</td><td>perun-1</td><td>cyberG 🟢</td><td>6152777</td><td>0</td><td>False</td><td>0</td><td>2023-12-05T09:55:54.414705945UTC</td></tr><tr><td>79.137.68.96:26657</td><td>perun-1</td><td>archive-node2 🟢</td><td>6152774</td><td>1</td><td>False</td><td>0</td><td>2023-12-05T09:55:37.124658304UTC</td></tr><tr><td>65.108.70.119:33657</td><td>perun-1</td><td>AlxVoy 🟢</td><td>6152777</td><td>1</td><td>False</td><td>0</td><td>2023-12-05T09:55:53.686170723UTC</td></tr><tr><td>149.202.66.111:26657</td><td>perun-1</td><td>archive-node1 🟢</td><td>6152780</td><td>1</td><td>False</td><td>0</td><td>2023-12-05T09:56:10.603326385UTC</td></tr><tr><td>185.245.182.192:46657</td><td>perun-1</td><td>Meerlabs 🔴</td><td>6152781</td><td>1051501</td><td>False</td><td>493550</td><td>2023-12-05T09:56:16.076884183UTC</td></tr><tr><td>185.215.167.18:26657</td><td>perun-1</td><td>Rawalot 🔴</td><td>6152783</td><td>1090501</td><td>False</td><td>579034</td><td>2023-12-05T09:56:28.512945498UTC</td></tr><tr><td>95.70.184.178:44657</td><td>perun-1</td><td>mahof 🔴</td><td>6152777</td><td>2342001</td><td>False</td><td>1357006</td><td>2023-12-05T09:55:52.899988879UTC</td></tr><tr><td>209.182.239.169:46657</td><td>perun-1</td><td>SECARD 🔴</td><td>6152779</td><td>2616101</td><td>False</td><td>675729</td><td>2023-12-05T09:56:07.959950104UTC</td></tr><tr><td>89.117.58.109:26657</td><td>perun-1</td><td>medes 🔴</td><td>6152782</td><td>2826001</td><td>False</td><td>471345</td><td>2023-12-05T09:56:23.216979449UTC</td></tr><tr><td>5.135.141.191:26657</td><td>perun-1</td><td>c4e-sentry1-mainnet 🟢</td><td>6152774</td><td>4267001</td><td>False</td><td>0</td><td>2023-12-05T09:55:36.414458780UTC</td></tr><tr><td>65.109.30.185:26657</td><td>perun-1</td><td>c4e-sentry2-mainnet 🟢</td><td>6152781</td><td>5186001</td><td>False</td><td>0</td><td>2023-12-05T09:56:15.721009327UTC</td></tr><tr><td>77.55.216.80:26657</td><td>perun-1</td><td>c4e-sentry4-mainnet 🟢</td><td>6152777</td><td>5187001</td><td>False</td><td>0</td><td>2023-12-05T09:55:53.305212148UTC</td></tr><tr><td>65.108.75.107:39657</td><td>perun-1</td><td>node 🟢</td><td>6152778</td><td>5198801</td><td>False</td><td>0</td><td>2023-12-05T09:55:56.813151946UTC</td></tr><tr><td>163.172.18.144:26657</td><td>perun-1</td><td>c4e-sentry3-mainnet 🟢</td><td>6152781</td><td>5286001</td><td>False</td><td>0</td><td>2023-12-05T09:56:16.711574776UTC</td></tr><tr><td>65.108.141.109:39657</td><td>perun-1</td><td>node 🟢</td><td>6152775</td><td>5303301</td><td>False</td><td>0</td><td>2023-12-05T09:55:39.530369866UTC</td></tr><tr><td>135.181.114.86:30657</td><td>perun-1</td><td>NodeName 🔴</td><td>6152780</td><td>5508301</td><td>False</td><td>333717</td><td>2023-12-05T09:56:10.949059258UTC</td></tr><tr><td>65.108.125.55:16557</td><td>perun-1</td><td>Validatrium-rpc 🟢</td><td>6152783</td><td>5551301</td><td>False</td><td>0</td><td>2023-12-05T09:56:25.642450593UTC</td></tr><tr><td>185.252.235.83:26657</td><td>perun-1</td><td>Alien 🔴</td><td>6152780</td><td>5736001</td><td>False</td><td>380508</td><td>2023-12-05T09:56:11.256087537UTC</td></tr><tr><td>38.242.220.64:16657</td><td>perun-1</td><td>mahof 🟢</td><td>6152780</td><td>5980001</td><td>False</td><td>0</td><td>2023-12-05T09:56:08.267255143UTC</td></tr><tr><td>65.108.66.174:30657</td><td>perun-1</td><td>hello-BccNodesRPC 🟢</td><td>6152777</td><td>5985401</td><td>False</td><td>0</td><td>2023-12-05T09:55:54.036613040UTC</td></tr><tr><td>135.181.133.249:13457</td><td>perun-1</td><td>StakeUp 🔴</td><td>6152773</td><td>6015001</td><td>False</td><td>1357007</td><td>2023-12-05T09:55:27.848783500UTC</td></tr><tr><td>168.119.226.107:26957</td><td>perun-1</td><td>c4e_rpc 🟢</td><td>6152776</td><td>6052775</td><td>False</td><td>0</td><td>2023-12-05T09:55:45.984431004UTC</td></tr><tr><td>65.108.124.219:31657</td><td>perun-1</td><td>MantiCore 🔴</td><td>6152777</td><td>6052777</td><td>False</td><td>837495</td><td>2023-12-05T09:55:52.490147221UTC</td></tr><tr><td>95.216.102.121:26657</td><td>perun-1</td><td>dteam 🟢</td><td>6152774</td><td>6145001</td><td>False</td><td>0</td><td>2023-12-05T09:55:36.756041681UTC</td></tr><tr><td>5.181.190.157:16657</td><td>perun-1</td><td>landeros-rpc 🟢</td><td>6152783</td><td>6148501</td><td>False</td><td>0</td><td>2023-12-05T09:56:28.136829915UTC</td></tr><tr><td>135.181.210.171:17097</td><td>perun-1</td><td>STAVR-Service 🟢</td><td>6152778</td><td>6151001</td><td>False</td><td>0</td><td>2023-12-05T09:55:59.209944954UTC</td></tr></table>
