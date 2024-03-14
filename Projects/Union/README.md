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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>95.217.107.96:26257</td><td>union-testnet-6</td><td>Staketab 🔴</td><td>433592</td><td>1</td><td>False</td><td>on</td><td>1000002</td><td>2024-03-14T03:44:34.212677558UTC</td></tr><tr><td>157.245.1.52:26657</td><td>union-testnet-6</td><td>poisonphang-val 🔴</td><td>433592</td><td>1</td><td>False</td><td>on</td><td>1000000</td><td>2024-03-14T03:44:34.818802789UTC</td></tr><tr><td>148.251.235.130:15657</td><td>union-testnet-6</td><td>Staketab-snap 🟢</td><td>433592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:35.362348451UTC</td></tr><tr><td>37.27.37.88:26657</td><td>union-testnet-6</td><td>kesgin 🟢</td><td>433592</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:35.690770863UTC</td></tr><tr><td>65.109.141.9:26657</td><td>union-testnet-6</td><td>Glang 🟢</td><td>433593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:40.108053506UTC</td></tr><tr><td>157.245.1.27:26657</td><td>union-testnet-6</td><td>poisonphang-seed 🟢</td><td>433593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:41.017030752UTC</td></tr><tr><td>198.244.182.197:26657</td><td>union-testnet-6</td><td>Lightshift 🔴</td><td>433594</td><td>1</td><td>False</td><td>on</td><td>1000000</td><td>2024-03-14T03:44:43.328587023UTC</td></tr><tr><td>84.247.177.24:26657</td><td>union-testnet-6</td><td>zero 🟢</td><td>433594</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:47.836424738UTC</td></tr><tr><td>213.239.214.73:26657</td><td>union-testnet-6</td><td>PFC 🔴</td><td>433595</td><td>1</td><td>False</td><td>on</td><td>1000001</td><td>2024-03-14T03:44:52.104281226UTC</td></tr><tr><td>178.128.225.129:26657</td><td>union-testnet-6</td><td>bonlulu 🔴</td><td>433595</td><td>1</td><td>False</td><td>on</td><td>1000000</td><td>2024-03-14T03:44:52.746370194UTC</td></tr><tr><td>65.108.54.139:26657</td><td>union-testnet-6</td><td>barsbaba 🟢</td><td>433595</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:53.062259729UTC</td></tr><tr><td>65.109.6.68:26657</td><td>union-testnet-6</td><td>biggreenreset 🟢</td><td>433596</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:55.432873116UTC</td></tr><tr><td>209.126.86.119:26657</td><td>union-testnet-6</td><td>Conqueror 🟢</td><td>433599</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:16.808040723UTC</td></tr><tr><td>167.235.25.11:26657</td><td>union-testnet-6</td><td>hubble 🟢</td><td>433600</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:23.188857376UTC</td></tr><tr><td>65.108.82.76:26657</td><td>union-testnet-6</td><td>hakanabi 🟢</td><td>433600</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:23.509314681UTC</td></tr><tr><td>65.108.40.246:26657</td><td>union-testnet-6</td><td>Synergy_Nodes 🔴</td><td>433601</td><td>1</td><td>False</td><td>on</td><td>1000001</td><td>2024-03-14T03:45:27.878737903UTC</td></tr><tr><td>84.247.169.208:26657</td><td>union-testnet-6</td><td>yy 🟢</td><td>433601</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:28.194798414UTC</td></tr><tr><td>198.244.179.173:26657</td><td>union-testnet-6</td><td>test 🔴</td><td>433602</td><td>1</td><td>False</td><td>on</td><td>1000001</td><td>2024-03-14T03:45:30.512166773UTC</td></tr><tr><td>195.88.87.81:26657</td><td>union-testnet-6</td><td>Contabo 🟢</td><td>433602</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:30.808086437UTC</td></tr><tr><td>65.108.156.104:26657</td><td>union-testnet-6</td><td>Senol 🟢</td><td>433602</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:31.105846834UTC</td></tr><tr><td>93.159.130.38:32657</td><td>union-testnet-6</td><td>bro 🟢</td><td>433602</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:45:31.384339805UTC</td></tr><tr><td>135.181.210.171:4257</td><td>union-testnet-6</td><td>STAVR-Service 🟢</td><td>433592</td><td>433001</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T03:44:35.136830946UTC</td></tr></table>
