<h1 align="center"> 🔥OKP4🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/OKP4)
=

# StateSync
```python
SNAP_RPC=http://okp.rpc.t.stavr.tech:10097
peers="3301c449cf9706c35a0fafb7b97d20e40cdb96df@okp.peer.stavr.tech:10096"
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.okp4d/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.okp4d/config/config.toml
okp4d tendermint unsafe-reset-all --home /root/.okp4d --keep-addr-book
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.okp4d/config/app.toml
systemctl restart okp4d && journalctl -u okp4d -f -o cat

```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop okp4d
cp $HOME/.okp4d/data/priv_validator_state.json $HOME/.okp4d/priv_validator_state.json.backup
rm -rf $HOME/.okp4d/data
curl -o - -L http://okp.snapshot.stavr.tech:1011/okp/okp-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.okp4d --strip-components 2
mv $HOME/.okp4d/priv_validator_state.json.backup $HOME/.okp4d/data/priv_validator_state.json
wget -O $HOME/.okp4d/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/OKP4/addrbook.json"
sudo systemctl restart okp4d && journalctl -u okp4d -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:          https://explorer.stavr.tech/OKP4-Testnet/staking        Indexer "ON" \
🔥API🔥:                       https://okp4.api.t.stavr.tech \
🔥RPC🔥:                      http://okp.rpc.t.stavr.tech:10097                  Snapshot-interval = 300 \
🔥gRPC🔥:                    http://okp.grpc.t.stavr.tech:8029 \
🔥peer🔥:                     `3301c449cf9706c35a0fafb7b97d20e40cdb96df@okp.peer.stavr.tech:10096` \
🔥Addrbook🔥:    ```wget -O $HOME/.okp4d/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/OKP4/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O okp https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/OKP4/okp && chmod +x okp && ./okp``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/OKP4/Decentralization)🔥

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

[raw json Testnet](https://rpc-check.okpt.stavr.tech/okpt/rpc-okpt-result.json)
=




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.21.170.3:42657</td><td>okp4-nemeton-1</td><td>Munris 🔴</td><td>6235180</td><td>1</td><td>False</td><td>on</td><td>611602</td><td>2024-01-29T16:19:01.508516340UTC</td></tr><tr><td>161.97.77.219:36657</td><td>okp4-nemeton-1</td><td>Apollo 🔴</td><td>6235181</td><td>3888601</td><td>False</td><td>on</td><td>41585</td><td>2024-01-29T16:19:03.886156974UTC</td></tr><tr><td>15.235.53.45:2031</td><td>okp4-nemeton-1</td><td>Zenscape 🔴</td><td>6235181</td><td>5086501</td><td>False</td><td>off</td><td>49653</td><td>2024-01-29T16:19:06.634281354UTC</td></tr><tr><td>213.239.207.175:38657</td><td>okp4-nemeton-1</td><td>landeros 🔴</td><td>6235180</td><td>5148001</td><td>False</td><td>off</td><td>139160</td><td>2024-01-29T16:19:00.835601184UTC</td></tr><tr><td>178.18.254.211:10657</td><td>okp4-nemeton-1</td><td>CosmoBook 🔴</td><td>6235180</td><td>5172801</td><td>False</td><td>off</td><td>266541</td><td>2024-01-29T16:18:58.339350497UTC</td></tr><tr><td>65.21.187.101:26657</td><td>okp4-nemeton-1</td><td>SmartHamster 🔴</td><td>6235174</td><td>5418606</td><td>False</td><td>on</td><td>489685</td><td>2024-01-29T16:18:29.425724550UTC</td></tr><tr><td>86.48.0.190:14657</td><td>okp4-nemeton-1</td><td>AnatolianService 🟢</td><td>6235177</td><td>5951001</td><td>False</td><td>off</td><td>0</td><td>2024-01-29T16:18:49.849554161UTC</td></tr><tr><td>38.242.251.204:36657</td><td>okp4-nemeton-1</td><td>Lexar 🔴</td><td>6235173</td><td>6028401</td><td>False</td><td>on</td><td>70786</td><td>2024-01-29T16:18:24.603752031UTC</td></tr><tr><td>65.21.90.141:12231</td><td>okp4-nemeton-1</td><td>SerGo 🔴</td><td>6235175</td><td>6135175</td><td>False</td><td>off</td><td>85485</td><td>2024-01-29T16:18:38.007568863UTC</td></tr><tr><td>65.108.131.190:23457</td><td>okp4-nemeton-1</td><td>okp4 🔴</td><td>6235176</td><td>6135176</td><td>False</td><td>off</td><td>611454</td><td>2024-01-29T16:18:40.690866036UTC</td></tr><tr><td>142.132.202.50:11111</td><td>okp4-nemeton-1</td><td>cryptobtcbuyer 🔴</td><td>6235176</td><td>6135176</td><td>False</td><td>off</td><td>134928</td><td>2024-01-29T16:18:41.254576074UTC</td></tr><tr><td>94.130.137.122:29657</td><td>okp4-nemeton-1</td><td>Vagif 🔴</td><td>6235180</td><td>6135180</td><td>False</td><td>off</td><td>456860</td><td>2024-01-29T16:19:00.621451767UTC</td></tr><tr><td>65.109.117.212:13091</td><td>okp4-nemeton-1</td><td>w3coins 🔴</td><td>6235181</td><td>6135181</td><td>False</td><td>off</td><td>20000</td><td>2024-01-29T16:19:07.038758362UTC</td></tr><tr><td>51.158.73.82:26657</td><td>okp4-nemeton-1</td><td>Meria 🟢</td><td>6235175</td><td>6226503</td><td>False</td><td>off</td><td>0</td><td>2024-01-29T16:18:38.291186430UTC</td></tr><tr><td>65.109.93.58:34657</td><td>okp4-nemeton-1</td><td>nj-snap 🟢</td><td>6235176</td><td>6232606</td><td>False</td><td>off</td><td>0</td><td>2024-01-29T16:18:41.035755391UTC</td></tr><tr><td>135.181.210.171:10097</td><td>okp4-nemeton-1</td><td>STAVR-Service 🟢</td><td>6235173</td><td>6233101</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T16:18:26.995122991UTC</td></tr></table>
