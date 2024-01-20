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
🔥Auto_install script Testnet🔥: ```wget -O juno-t https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Juno/Testnet/juno-t && chmod +x juno-t && ./juno-t``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Juno/Decentralization)🔥

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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>93.189.27.177:26657</td><td>juno-1</td><td>blockpitnode 🟢</td><td>13261726</td><td>9074001</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:03:01.672372236UTC</td></tr><tr><td>66.172.36.140:11657</td><td>juno-1</td><td>node 🟢</td><td>13261725</td><td>11389910</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:03:05.485389234UTC</td></tr><tr><td>148.113.159.221:36657</td><td>juno-1</td><td>thick_boi 🟢</td><td>12265007</td><td>11722438</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:02:31.100111599UTC</td></tr><tr><td>65.108.98.235:38857</td><td>juno-1</td><td>sentry-4 🟢</td><td>13261701</td><td>11772968</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:01:36.889015229UTC</td></tr><tr><td>135.181.1.44:26657</td><td>juno-1</td><td>rpc-3 🟢</td><td>13261706</td><td>12279533</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:01:55.741699770UTC</td></tr><tr><td>141.94.195.104:26657</td><td>juno-1</td><td>rpc-8 🟢</td><td>13261713</td><td>12279533</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:02:17.408064861UTC</td></tr><tr><td>65.21.74.247:24657</td><td>juno-1</td><td>#SoloNation 🔴</td><td>13261698</td><td>12379123</td><td>False</td><td>on</td><td>2604</td><td>2024-01-20T07:01:25.718863757UTC</td></tr><tr><td>213.239.213.142:12657</td><td>juno-1</td><td>BRAND-juno-relayer 🟢</td><td>13261653</td><td>12429275</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T06:58:58.149242092UTC</td></tr><tr><td>66.172.36.139:11657</td><td>juno-1</td><td>node 🟢</td><td>13261652</td><td>12454834</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T06:58:51.661819399UTC</td></tr><tr><td>65.108.44.124:36010</td><td>juno-1</td><td>bricks_juno 🟢</td><td>13261709</td><td>12480440</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:02:04.426403172UTC</td></tr><tr><td>57.128.20.238:34657</td><td>juno-1</td><td>rpc 🟢</td><td>13261714</td><td>12683032</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:02:19.992564506UTC</td></tr><tr><td>194.163.172.115:12657</td><td>juno-1</td><td>Stake&Relax-juno-main 🟢</td><td>13261700</td><td>12932001</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:01:34.353900412UTC</td></tr><tr><td>142.132.253.13:49657</td><td>juno-1</td><td>rpcs 🟢</td><td>13261675</td><td>12960671</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:00:09.568026329UTC</td></tr><tr><td>95.168.173.33:18657</td><td>juno-1</td><td>JUNO-mainnet-prod 🔴</td><td>13261765</td><td>13011765</td><td>False</td><td>on</td><td>5943</td><td>2024-01-20T07:05:17.501757818UTC</td></tr><tr><td>135.181.210.171:1067</td><td>juno-1</td><td>STAVR-Service 🟢</td><td>13261752</td><td>13033964</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:04:31.586586600UTC</td></tr><tr><td>138.201.21.121:24957</td><td>juno-1</td><td>Validatrium-rpc 🟢</td><td>13261641</td><td>13084801</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T06:58:19.533212302UTC</td></tr><tr><td>65.108.125.93:26657</td><td>juno-1</td><td>juno 🟢</td><td>13261668</td><td>13110265</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T06:59:48.706410116UTC</td></tr><tr><td>75.26.237.223:36657</td><td>juno-1</td><td>test 🟢</td><td>13261731</td><td>13142921</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:03:22.699319151UTC</td></tr><tr><td>176.9.139.74:36657</td><td>juno-1</td><td>myrpc 🟢</td><td>13261727</td><td>13186740</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:03:02.252498176UTC</td></tr><tr><td>65.108.40.61:28657</td><td>juno-1</td><td>29391 🟢</td><td>13261682</td><td>13237589</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:00:35.565554088UTC</td></tr><tr><td>202.65.150.1:1528</td><td>juno-1</td><td>snap 🟢</td><td>13261719</td><td>13254225</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T07:02:40.492240954UTC</td></tr></table>
