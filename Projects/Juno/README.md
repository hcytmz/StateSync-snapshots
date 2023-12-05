<h1 align="center"> 🔥JUNO🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Juno)
=

<h1 align="center"> MAINNET</h1>

# StateSync Juno Mainnet
```python
SNAP_RPC=http://juno.rpc.m.stavr.tech:1067
PEERS="9ec270e1b4cdd38557da9d374ae4333145ee9300@juno.peer.stavr.tech:1066"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.juno/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.juno/config/config.toml
junod tendermint unsafe-reset-all
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.juno/config/app.toml
curl -o - -L http://juno.wasm.stavr.tech:1005/wasm-juno.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
sudo systemctl restart junod && journalctl -u junod -f -o cat
```
# SnapShot (~12 GB) updated every 12 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop junod
cp $HOME/.juno/data/priv_validator_state.json $HOME/.juno/priv_validator_state.json.backup
rm -rf $HOME/.juno/data
curl -o - -L http://juno.snapshot.stavr.tech:1024/juno/juno-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno --strip-components 2
curl -o - -L http://juno.wasm.stavr.tech:1005/wasm-juno.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
mv $HOME/.juno/priv_validator_state.json.backup $HOME/.juno/data/priv_validator_state.json
wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/addrbook.json"
sudo systemctl restart junod && journalctl -u junod -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Juno/Testnet)
=

# StateSync Juno Testnet (Temporarily stopped)
```python
SNAP_RPC=http://juno.rpc.t.stavr.tech:1067
PEERS="518d31bf039289b6c8d8defd7e9509d8e28b7cd3@junot.peer.stavr.tech:1066"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.juno/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.juno/config/config.toml
junod tendermint unsafe-reset-all --home $HOME/.juno
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.juno/config/app.toml
curl -o - -L http://juno-t.wasm.stavr.tech:1001/wasm-junot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
sudo systemctl restart junod && journalctl -u junod -f -o cat
```

# SnapShot (~5GB) updated every 5 hours (Temporarily stopped)
```python
cd $HOME
snap install lz4
sudo systemctl stop junod
cp $HOME/.juno/data/priv_validator_state.json $HOME/.juno/priv_validator_state.json.backup
rm -rf $HOME/.juno/data
curl -o - -L http://junot.snapshot.stavr.tech:1030/junot/junot-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno --strip-components 2
curl -o - -L http://juno-t.wasm.stavr.tech:1001/wasm-junot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2
mv $HOME/.juno/priv_validator_state.json.backup $HOME/.juno/data/priv_validator_state.json
wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/addrbook.json"
sudo systemctl restart junod && journalctl -u junod -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Juno/staking		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Juno-Testnet/staking       `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://juno.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://juno.api.t.stavr.tech \
🔥RPC Mainnet🔥:           http://juno.rpc.m.stavr.tech:1067              `Snapshot-interval = 1000` \
🔥RPC Testnet🔥:           http://juno.rpc.t.stavr.tech:1067              `Snapshot-interval = 1000` \
🔥gRPC Mainnet🔥:          http://juno.grpc.m.stavr.tech:504 \
🔥gRPC Testnet🔥:          http://juno.grpc.t.stavr.tech:504 \
🔥peer Mainnet🔥:					 `9ec270e1b4cdd38557da9d374ae4333145ee9300@juno.peer.stavr.tech:1066` \
🔥peer Testnet🔥:					 `eb4cbf9bfea70a9e02baffbe35df02f073c70049@junot.peer.stavr.tech:1066` \
🔥WASM Mainnet🔥: 		 ```curl -o - -L http://juno.wasm.stavr.tech:1005/wasm-juno.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2```		`updated every 10 minutes` \
🔥WASM Testnet🔥: 		 ```curl -o - -L http://juno-t.wasm.stavr.tech:1001/wasm-junot.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.juno/ --strip-components 2```   `updated every 5 minutes` \
🔥Genesis Mainnet🔥:     ```wget -O $HOME/.juno/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/genesis.json"``` \
🔥Genesis Testnet🔥:	 ```wget -O $HOME/.juno/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/genesis.json"``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.juno/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O jun https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/jun && chmod +x jun && ./jun``` \
🔥Auto_install script Testnet🔥: ```wget -O juno-t https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/juno-t && chmod +x juno-t && ./juno-t```

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

[raw json Mainnet](https://rpc-check.junom.stavr.tech/junom/rpc-junom-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Juno/Rpc-Check-Testnet)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.181.5.176:26657</td><td>juno-1</td><td>ZenChainLabs-RPC 🟢</td><td>11389693</td><td>4136532</td><td>False</td><td>0</td><td>2023-12-05T13:10:06.107790709UTC</td></tr><tr><td>95.217.202.49:34657</td><td>juno-1</td><td>rpc 🟢</td><td>12109557</td><td>11389910</td><td>False</td><td>0</td><td>2023-12-05T13:09:16.605059121UTC</td></tr><tr><td>66.172.36.140:11657</td><td>juno-1</td><td>node 🟢</td><td>12109595</td><td>11389910</td><td>False</td><td>0</td><td>2023-12-05T13:11:20.845759244UTC</td></tr><tr><td>176.9.139.74:36657</td><td>juno-1</td><td>myrpc 🟢</td><td>12109594</td><td>11395001</td><td>False</td><td>0</td><td>2023-12-05T13:11:17.850318373UTC</td></tr><tr><td>213.239.213.142:12657</td><td>juno-1</td><td>BRAND-juno-relayer 🟢</td><td>12109556</td><td>11395600</td><td>False</td><td>0</td><td>2023-12-05T13:09:07.487509117UTC</td></tr><tr><td>135.181.1.44:26657</td><td>juno-1</td><td>rpc-3 🟢</td><td>12109584</td><td>11395600</td><td>False</td><td>0</td><td>2023-12-05T13:10:39.804617892UTC</td></tr><tr><td>141.94.195.104:26657</td><td>juno-1</td><td>rpc-8 🟢</td><td>12109586</td><td>11395600</td><td>False</td><td>0</td><td>2023-12-05T13:10:52.698465683UTC</td></tr><tr><td>65.109.61.50:26657</td><td>juno-1</td><td>rpc-1 🟢</td><td>12109591</td><td>11395600</td><td>False</td><td>0</td><td>2023-12-05T13:11:05.614107337UTC</td></tr><tr><td>138.201.21.121:24957</td><td>juno-1</td><td>Validatrium-rpc 🟢</td><td>12109547</td><td>11596170</td><td>False</td><td>0</td><td>2023-12-05T13:08:41.551450367UTC</td></tr><tr><td>65.109.113.86:26657</td><td>juno-1</td><td>bricks_juno 🟢</td><td>12109568</td><td>11621313</td><td>False</td><td>0</td><td>2023-12-05T13:09:46.870120234UTC</td></tr><tr><td>23.111.152.170:27657</td><td>juno-1</td><td>OranG3cluB 🟢</td><td>12109563</td><td>11646585</td><td>False</td><td>0</td><td>2023-12-05T13:09:33.782064840UTC</td></tr><tr><td>66.172.36.139:11657</td><td>juno-1</td><td>node 🟢</td><td>12109554</td><td>11728921</td><td>False</td><td>0</td><td>2023-12-05T13:09:05.056256761UTC</td></tr><tr><td>83.53.145.27:19657</td><td>juno-1</td><td>Validavia 🟢</td><td>12109591</td><td>11747704</td><td>False</td><td>0</td><td>2023-12-05T13:11:07.004657731UTC</td></tr><tr><td>95.168.173.33:18657</td><td>juno-1</td><td>JUNO-mainnet-prod 🔴</td><td>12109618</td><td>11954501</td><td>False</td><td>6772</td><td>2023-12-05T13:12:37.679284763UTC</td></tr><tr><td>194.163.172.115:12657</td><td>juno-1</td><td>Stake&Relax-juno-main 🟢</td><td>12109580</td><td>12050001</td><td>False</td><td>0</td><td>2023-12-05T13:10:29.106034398UTC</td></tr><tr><td>135.181.210.171:1067</td><td>juno-1</td><td>STAVR-Service 🟢</td><td>12109612</td><td>12053233</td><td>False</td><td>0</td><td>2023-12-05T13:12:16.629620857UTC</td></tr><tr><td>202.65.150.1:1528</td><td>juno-1</td><td>snap 🟢</td><td>12109591</td><td>12108331</td><td>False</td><td>0</td><td>2023-12-05T13:11:06.537836325UTC</td></tr></table>