<h1 align="center"> 🔥BITCANNA MAINNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Bitcanna)
=

# StateSync
```python
RPC="http://bitcanna.rpc.m.stavr.tech:21327"
peers="644ac886e7f2fe082b3556dc694076e71a4e959a@bitcanna.peers.stavr.tech:21326"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.bcna/config/config.toml
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.bcna/config/config.toml
sudo systemctl stop bcnad && bcnad tendermint unsafe-reset-all --keep-addr-book
sudo systemctl restart bcnad && sudo journalctl -u bcnad -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop bcnad
cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup
rm -rf $HOME/.bcna/data
curl -o - -L http://bitcanna.snapshot.stavr.tech:1004/bca/bca-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bcna --strip-components 2
mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json
wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/addrbook.json"
sudo systemctl restart bcnad && journalctl -u bcnad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:    https://explorer.stavr.tech/Bitcanna/staking          `Indexer "ON"` \
🔥EXPLORER Devnet🔥:     https://explorer.stavr.tech/Bitcanna-DEV/staking     `Indexer "ON"` \
🔥API Mainnet🔥:         https://bitcanna.api.m.stavr.tech \
🔥API Devnet🔥:          https://bitcanna.api.dev.stavr.tech \
🔥RPC Mainnet🔥:         http://bitcanna.rpc.m.stavr.tech:21327         `Snapshot-interval = 300` \
🔥gRPC Mainnet🔥:        http://bitcanna.grpc.m.stavr.tech:9081 \
🔥gRPC Devnet🔥:**       http://bitcanna.grpc.dev.stavr.tech:2901 \
🔥peer Mainnet🔥:        `644ac886e7f2fe082b3556dc694076e71a4e959a@bitcanna.peers.stavr.tech:21326` \
🔥peer Devnet🔥:         `b0c7e5c69aaf00626baaf7c59370029b587a91a4@bitcannadev.peers.stavr.tech:30006` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/addrbook.json"``` \
🔥Addrbook Devnet🔥:    ```wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/Bitcanna_DEV/addrbook.json"``` \
🔥Auto_install script Mainnet🔥:```wget -O bitcanna https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/bitcanna && chmod +x bitcanna && ./bitcanna```



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

[raw json](https://rpc-check.bcam.stavr.tech/bcam/rpc-bcam-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>1370881</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T10:28:14.796969196UTC</td></tr><tr><td>85.190.246.173:33657</td><td>froopyland_100-1</td><td>yatko 🟢</td><td>1370882</td><td>1</td><td>False</td><td>0</td><td>2023-11-22T10:28:24.459156167UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>1370883</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T10:28:29.646580802UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>1370885</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T10:28:41.990290871UTC</td></tr><tr><td>161.97.180.20:26657</td><td>froopyland_100-1</td><td>Blockscope.net 🔴</td><td>1370886</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T10:28:46.900133672UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>1370886</td><td>1</td><td>False</td><td>1</td><td>2023-11-22T10:28:47.328642574UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🟢</td><td>1370886</td><td>1</td><td>False</td><td>0</td><td>2023-11-22T10:28:47.672679524UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>1370881</td><td>106001</td><td>False</td><td>1</td><td>2023-11-22T10:28:15.476866656UTC</td></tr><tr><td>89.116.31.118:26657</td><td>froopyland_100-1</td><td>cardex 🟢</td><td>1370882</td><td>293001</td><td>False</td><td>0</td><td>2023-11-22T10:28:21.994086224UTC</td></tr><tr><td>78.46.103.246:56657</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>1370880</td><td>407001</td><td>False</td><td>1</td><td>2023-11-22T10:28:11.317114729UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>1370884</td><td>591001</td><td>False</td><td>0</td><td>2023-11-22T10:28:34.066739837UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>1370884</td><td>737456</td><td>False</td><td>1</td><td>2023-11-22T10:28:34.421629393UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>1370884</td><td>737456</td><td>False</td><td>1</td><td>2023-11-22T10:28:34.823525681UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>1370879</td><td>820001</td><td>False</td><td>0</td><td>2023-11-22T10:28:03.392428403UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>1370884</td><td>922548</td><td>False</td><td>1</td><td>2023-11-22T10:28:35.134410609UTC</td></tr><tr><td>85.239.240.194:33657</td><td>froopyland_100-1</td><td>zardozmonopoly 🟢</td><td>1370887</td><td>935165</td><td>False</td><td>0</td><td>2023-11-22T10:28:53.614873161UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>1370885</td><td>1006001</td><td>False</td><td>1</td><td>2023-11-22T10:28:41.602274973UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>1370883</td><td>1070883</td><td>False</td><td>0</td><td>2023-11-22T10:28:26.842847157UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>1370887</td><td>1150548</td><td>False</td><td>1</td><td>2023-11-22T10:28:50.017638081UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>1370880</td><td>1158907</td><td>False</td><td>1</td><td>2023-11-22T10:28:12.377405809UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1370878</td><td>1238063</td><td>False</td><td>0</td><td>2023-11-22T10:27:58.446091996UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1370886</td><td>1318001</td><td>False</td><td>0</td><td>2023-11-22T10:28:44.403466729UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>1370879</td><td>1330001</td><td>False</td><td>1</td><td>2023-11-22T10:28:03.677341301UTC</td></tr><tr><td>20.122.112.2:36657</td><td>froopyland_100-1</td><td>dymdtestnet 🟢</td><td>1361906</td><td>1339001</td><td>False</td><td>0</td><td>2023-11-22T10:28:06.384487887UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>1370883</td><td>1360001</td><td>False</td><td>1</td><td>2023-11-22T10:28:27.239323085UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>1370879</td><td>1368573</td><td>False</td><td>0</td><td>2023-11-22T10:28:06.840813726UTC</td></tr></table>
