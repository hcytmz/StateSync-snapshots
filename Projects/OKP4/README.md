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




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.21.170.3:42657</td><td>okp4-nemeton-1</td><td>Munris 🔴</td><td>5964266</td><td>1</td><td>False</td><td>on</td><td>558261</td><td>2024-01-12T07:59:03.391141901UTC</td></tr><tr><td>136.243.88.91:6041</td><td>okp4-nemeton-1</td><td>Enigma 🔴</td><td>5964267</td><td>1123444</td><td>False</td><td>off</td><td>10003</td><td>2024-01-12T07:59:08.120690620UTC</td></tr><tr><td>38.242.251.204:36657</td><td>okp4-nemeton-1</td><td>Lexar 🔴</td><td>5964257</td><td>3052301</td><td>False</td><td>on</td><td>71500</td><td>2024-01-12T07:58:20.467916872UTC</td></tr><tr><td>161.97.77.219:36657</td><td>okp4-nemeton-1</td><td>Apollo 🔴</td><td>5964266</td><td>3888601</td><td>False</td><td>on</td><td>41581</td><td>2024-01-12T07:59:05.783161940UTC</td></tr><tr><td>15.235.53.45:2031</td><td>okp4-nemeton-1</td><td>Zenscape 🔴</td><td>5964267</td><td>5086501</td><td>False</td><td>off</td><td>49653</td><td>2024-01-12T07:59:08.879799605UTC</td></tr><tr><td>213.239.207.175:38657</td><td>okp4-nemeton-1</td><td>landeros 🔴</td><td>5964266</td><td>5148001</td><td>False</td><td>off</td><td>139159</td><td>2024-01-12T07:59:02.685197649UTC</td></tr><tr><td>178.18.254.211:10657</td><td>okp4-nemeton-1</td><td>CosmoBook 🔴</td><td>5964265</td><td>5172801</td><td>False</td><td>off</td><td>266541</td><td>2024-01-12T07:59:00.015280761UTC</td></tr><tr><td>65.21.187.101:26657</td><td>okp4-nemeton-1</td><td>SmartHamster 🔴</td><td>5964258</td><td>5418606</td><td>False</td><td>on</td><td>452685</td><td>2024-01-12T07:58:25.286641325UTC</td></tr><tr><td>51.158.73.82:26657</td><td>okp4-nemeton-1</td><td>Meria 🔴</td><td>5964261</td><td>5804104</td><td>False</td><td>off</td><td>9510</td><td>2024-01-12T07:58:36.391112858UTC</td></tr><tr><td>65.21.90.141:12231</td><td>okp4-nemeton-1</td><td>SerGo 🔴</td><td>5964261</td><td>5864261</td><td>False</td><td>off</td><td>85482</td><td>2024-01-12T07:58:36.075918489UTC</td></tr><tr><td>65.108.131.190:23457</td><td>okp4-nemeton-1</td><td>okp4 🔴</td><td>5964262</td><td>5864262</td><td>False</td><td>off</td><td>558138</td><td>2024-01-12T07:58:42.913061956UTC</td></tr><tr><td>142.132.202.50:11111</td><td>okp4-nemeton-1</td><td>cryptobtcbuyer 🔴</td><td>5964263</td><td>5864263</td><td>False</td><td>off</td><td>134928</td><td>2024-01-12T07:58:45.294291711UTC</td></tr><tr><td>94.130.137.122:29657</td><td>okp4-nemeton-1</td><td>Vagif 🔴</td><td>5964266</td><td>5864266</td><td>False</td><td>off</td><td>436218</td><td>2024-01-12T07:59:02.418249293UTC</td></tr><tr><td>65.109.117.212:13091</td><td>okp4-nemeton-1</td><td>w3coins 🔴</td><td>5964267</td><td>5864267</td><td>False</td><td>off</td><td>20000</td><td>2024-01-12T07:59:09.345119994UTC</td></tr><tr><td>135.181.210.171:10097</td><td>okp4-nemeton-1</td><td>STAVR-Service 🟢</td><td>5964257</td><td>5962001</td><td>False</td><td>on</td><td>0</td><td>2024-01-12T07:58:22.833592367UTC</td></tr></table>
