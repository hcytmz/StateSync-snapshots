<h1 align="center"> 🔥Union🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Union)
=

<h1 align="center"> TESTNET</h1>

# StateSync union Testnet
```python
SNAP_RPC=https://union.rpc.t.stavr.tech:443
peers="59d554ab6bee4d814afb3e15af4031df19b2084c@union-t.seed.stavr.tech:4256"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.union/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.union/config/config.toml
uniond tendermint unsafe-reset-all --home /root/.union
wget -O $HOME/.union/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Union/addrbook.json"
systemctl restart uniond && journalctl -u uniond -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop uniond
cp $HOME/.union/data/priv_validator_state.json $HOME/.union/priv_validator_state.json.backup
rm -rf $HOME/.union/data
curl -o - -L https://union-t.snapshot.stavr.tech/union-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.union --strip-components 2
curl -o - -L https://union-t.wasm.stavr.tech/wasm-union.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.union --strip-components 2
mv $HOME/.union/priv_validator_state.json.backup $HOME/.union/data/priv_validator_state.json
wget -O $HOME/.union/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Union/addrbook.json"
sudo systemctl restart uniond && journalctl -u uniond -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Union-Testnet/        `Indexer "ON"` \
🔥API🔥:      https://union.api.t.stavr.tech \
🔥RPC🔥:      https://union.rpc.t.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:     http://union.grpc.t.stavr.tech:1901 \
🔥peer🔥:     `59d554ab6bee4d814afb3e15af4031df19b2084c@union-t.seed.stavr.tech:4256` \
🔥Genesis🔥:     `wget -O $HOME/.union/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Union/genesis.json"` \
🔥Addrbook🔥: ```wget -O $HOME/.union/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Union/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O uniont https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Union/uniont && chmod +x uniont && ./uniont`

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

[raw Testnet json](https://rpc-check.uniont.stavr.tech/uniont/rpc-uniont-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>95.217.107.96:26257</td><td>union-testnet-6</td><td>Staketab 🔴</td><td>269901</td><td>1</td><td>False</td><td>on</td><td>1000002</td><td>2024-03-02T12:15:32.719129011UTC</td></tr><tr><td>157.245.1.52:26657</td><td>union-testnet-6</td><td>poisonphang-val 🔴</td><td>269901</td><td>1</td><td>False</td><td>on</td><td>1000000</td><td>2024-03-02T12:15:33.327893289UTC</td></tr><tr><td>148.251.235.130:15657</td><td>union-testnet-6</td><td>Staketab-snap 🟢</td><td>269902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:33.872734406UTC</td></tr><tr><td>37.27.37.88:26657</td><td>union-testnet-6</td><td>kesgin 🟢</td><td>269902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:34.214866961UTC</td></tr><tr><td>65.109.141.9:26657</td><td>union-testnet-6</td><td>Glang 🟢</td><td>269902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:38.633561768UTC</td></tr><tr><td>80.79.6.154:26657</td><td>union-testnet-6</td><td>Numisma 🟢</td><td>237419</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:39.153842138UTC</td></tr><tr><td>157.245.1.27:26657</td><td>union-testnet-6</td><td>poisonphang-seed 🟢</td><td>269902</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:39.788108263UTC</td></tr><tr><td>198.244.182.197:26657</td><td>union-testnet-6</td><td>Lightshift 🔴</td><td>269903</td><td>1</td><td>False</td><td>on</td><td>1000000</td><td>2024-03-02T12:15:42.158734475UTC</td></tr><tr><td>84.247.177.24:26657</td><td>union-testnet-6</td><td>zero 🟢</td><td>269904</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:50.956131326UTC</td></tr><tr><td>213.239.214.73:26657</td><td>union-testnet-6</td><td>PFC 🔴</td><td>269905</td><td>1</td><td>False</td><td>on</td><td>1000001</td><td>2024-03-02T12:15:55.303929407UTC</td></tr><tr><td>178.128.225.129:26657</td><td>union-testnet-6</td><td>bonlulu 🔴</td><td>269905</td><td>1</td><td>False</td><td>on</td><td>1000000</td><td>2024-03-02T12:15:55.982183091UTC</td></tr><tr><td>65.108.54.139:26657</td><td>union-testnet-6</td><td>barsbaba 🟢</td><td>269905</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:56.307771943UTC</td></tr><tr><td>65.109.6.68:26657</td><td>union-testnet-6</td><td>biggreenreset 🟢</td><td>269905</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:56.649642137UTC</td></tr><tr><td>80.79.6.173:26657</td><td>union-testnet-6</td><td>CryptoKozaky 🟢</td><td>267587</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:15:59.112107379UTC</td></tr><tr><td>209.126.86.119:26657</td><td>union-testnet-6</td><td>Conqueror 🟢</td><td>269909</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:16:18.146571007UTC</td></tr><tr><td>167.235.25.11:26657</td><td>union-testnet-6</td><td>hubble 🟢</td><td>269910</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:16:22.520839392UTC</td></tr><tr><td>65.108.82.76:26657</td><td>union-testnet-6</td><td>hakanabi 🟢</td><td>269910</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:16:22.878985539UTC</td></tr><tr><td>65.108.40.246:26657</td><td>union-testnet-6</td><td>Synergy_Nodes 🔴</td><td>269911</td><td>1</td><td>False</td><td>on</td><td>1000001</td><td>2024-03-02T12:16:29.344553252UTC</td></tr><tr><td>84.247.169.208:26657</td><td>union-testnet-6</td><td>yy 🟢</td><td>226743</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:16:29.804931455UTC</td></tr><tr><td>198.244.179.173:26657</td><td>union-testnet-6</td><td>test 🔴</td><td>269911</td><td>1</td><td>False</td><td>on</td><td>1</td><td>2024-03-02T12:16:32.122879352UTC</td></tr><tr><td>65.108.156.104:26657</td><td>union-testnet-6</td><td>Senol 🟢</td><td>269911</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-02T12:16:32.460419864UTC</td></tr></table>
