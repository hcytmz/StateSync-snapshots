<h1 align="center"> 🔥LAMBDA MAINNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Lambda)
=


# StateSync
```python
SNAP_RPC=http://lambda.rpc.m.stavr.tech:31327
peers="ebdd47f7babb184240258d2fc6fba61bd994edaa@lambda.peer.stavr.tech:31326" 
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.lambdavm/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.lambdavm/config/config.toml
lambdavm tendermint unsafe-reset-all --home $HOME/.lambdavm
systemctl restart lambdavm && journalctl -u lambdavm -f -o cat

```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop lambdavm
cp $HOME/.lambdavm/data/priv_validator_state.json $HOME/.lambdavm/priv_validator_state.json.backup
rm -rf $HOME/.lambdavm/data
curl -o - -L http://lambda.snapshot.stavr.tech:5016/lambda/lambda-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lambdavm --strip-components 2
mv $HOME/.lambdavm/priv_validator_state.json.backup $HOME/.lambdavm/data/priv_validator_state.json
wget -O $HOME/.lambdavm/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lambda/addrbook.json"
sudo systemctl restart lambdavm && sudo journalctl -u lambdavm -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:      https://explorer.stavr.tech/Lambda/staking	        `Indexer "ON"` \
🔥API🔥: 			 		 https://lambda.api.m.stavr.tech \
🔥RPC🔥:           http://lambda.rpc.m.stavr.tech:31327	              `Snapshot-interval = 100` \
🔥gRPC🔥:          http://lambda.grpc.m.stavr.tech:2287 \
🔥peer🔥:					 `ebdd47f7babb184240258d2fc6fba61bd994edaa@lambda.peer.stavr.tech:31326` \
🔥Addrbook🔥:    ```wget -O $HOME/.lambdavm/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lambda/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O lamb https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Lambda/lamb && chmod +x lamb && ./lamb```


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

[raw json Mainnet](https://rpc-check.lambm.stavr.tech/lambm/rpc-lambm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>13.229.162.168:26657</td><td>lambda_92000-1</td><td>genesis2 🔴</td><td>10664180</td><td>1</td><td>False</td><td>on</td><td>16647031</td><td>2023-12-21T03:35:01.453360189UTC</td></tr><tr><td>13.213.214.88:26657</td><td>lambda_92000-1</td><td>genesis1 🔴</td><td>10664181</td><td>1</td><td>False</td><td>on</td><td>107835</td><td>2023-12-21T03:35:05.744729646UTC</td></tr><tr><td>65.109.84.19:26008</td><td>lambda_92000-1</td><td>bricks_lamb 🟢</td><td>7715743</td><td>7581001</td><td>False</td><td>on</td><td>0</td><td>2023-12-21T03:35:16.885355300UTC</td></tr><tr><td>65.21.141.82:21657</td><td>lambda_92000-1</td><td>kokos 🔴</td><td>10664182</td><td>7716001</td><td>False</td><td>off</td><td>546765</td><td>2023-12-21T03:35:08.148853586UTC</td></tr><tr><td>213.239.207.175:33657</td><td>lambda_92000-1</td><td>landeros 🔴</td><td>10664179</td><td>8136001</td><td>False</td><td>off</td><td>936892</td><td>2023-12-21T03:34:55.700500344UTC</td></tr><tr><td>65.109.88.254:29657</td><td>lambda_92000-1</td><td>ksalab 🔴</td><td>10664182</td><td>8715001</td><td>False</td><td>on</td><td>503508</td><td>2023-12-21T03:35:11.088497423UTC</td></tr><tr><td>38.242.220.64:26657</td><td>lambda_92000-1</td><td>mahof 🔴</td><td>10664177</td><td>10131001</td><td>False</td><td>off</td><td>770350</td><td>2023-12-21T03:34:50.996009997UTC</td></tr><tr><td>185.215.167.227:13657</td><td>lambda_92000-1</td><td>MAHOF 🔴</td><td>10664181</td><td>10134001</td><td>False</td><td>on</td><td>2051510</td><td>2023-12-21T03:35:04.750960718UTC</td></tr><tr><td>130.255.170.126:36657</td><td>lambda_92000-1</td><td>Sr20de 🔴</td><td>10664179</td><td>10353001</td><td>False</td><td>off</td><td>671452</td><td>2023-12-21T03:34:56.167050928UTC</td></tr><tr><td>23.88.91.115:26101</td><td>lambda_92000-1</td><td>RedHead 🔴</td><td>10664179</td><td>10564179</td><td>False</td><td>off</td><td>553202</td><td>2023-12-21T03:34:56.408419114UTC</td></tr><tr><td>65.21.90.141:12121</td><td>lambda_92000-1</td><td>SerGo 🔴</td><td>10664182</td><td>10564182</td><td>False</td><td>off</td><td>10551682</td><td>2023-12-21T03:35:11.432994665UTC</td></tr><tr><td>88.198.32.17:26657</td><td>lambda_92000-1</td><td>n0ok[MC] 🔴</td><td>10664183</td><td>10564183</td><td>False</td><td>off</td><td>1578630</td><td>2023-12-21T03:35:16.527885600UTC</td></tr><tr><td>135.181.210.171:31327</td><td>lambda_92000-1</td><td>STAVR-Service 🟢</td><td>10664182</td><td>10663001</td><td>False</td><td>on</td><td>0</td><td>2023-12-21T03:35:10.675206365UTC</td></tr></table>
