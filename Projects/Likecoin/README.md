<h1 align="center"> 🔥LikeCoin🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Likecoin)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://like.rpc.m.stavr.tech:443
SEEDS=fd7589625f4ad41bb93f96f4c962ed6638426497@like.peer.stavr.tech:1006
cp $HOME/.liked/data/priv_validator_state.json $HOME/.liked/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.liked/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.liked/config/config.toml
liked tendermint unsafe-reset-all --home $HOME/.liked --keep-addr-book
mv $HOME/.liked/priv_validator_state.json.backup $HOME/.liked/data/priv_validator_state.json
wget -O $HOME/.liked/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/addrbook.json"
sudo systemctl restart liked && journalctl -u liked -f -o cat
```
# SnapShot (~50 GB) updated every 24 hours
```python
SOON
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Likecoin-M        `Indexer "ON"` \
🔥API🔥:          https://like.api.m.stavr.tech \
🔥RPC🔥:          https://like.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://like.grpc.m.stavr.tech:2000 \
🔥peer🔥:         `fd7589625f4ad41bb93f96f4c962ed6638426497@like.peer.stavr.tech:1006` \
🔥Addrbook🔥:  `wget -O $HOME/.liked/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.liked/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/genesis.json"` \
🔥Auto_install script🔥:`wget -O likem https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Likecoin/likem && chmod +x likem && ./likem` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Likecoin/Decentralization)🔥


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

[raw Mainnet json](https://rpc-check.likem.stavr.tech/likem/rpc-likem-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>34.66.248.218:26657</td><td>likecoin-mainnet-2</td><td>dataxStaking 🔴</td><td>12862811</td><td>1</td><td>False</td><td>on</td><td>21820776214</td><td>2024-01-29T02:41:29.534476605UTC</td></tr><tr><td>203.135.141.208:26657</td><td>likecoin-mainnet-2</td><td>YasuArchive01 🟢</td><td>12862813</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T02:41:42.334245654UTC</td></tr><tr><td>154.53.63.22:26657</td><td>likecoin-mainnet-2</td><td>martianforest 🔴</td><td>12862814</td><td>1</td><td>False</td><td>on</td><td>563919907</td><td>2024-01-29T02:41:45.943700596UTC</td></tr><tr><td>144.126.131.195:26657</td><td>likecoin-mainnet-2</td><td>WeLike 🔴</td><td>12862810</td><td>5101130</td><td>False</td><td>on</td><td>116690668285</td><td>2024-01-29T02:41:19.763422572UTC</td></tr><tr><td>188.166.226.230:26657</td><td>likecoin-mainnet-2</td><td>PM 🔴</td><td>12862814</td><td>7730955</td><td>False</td><td>on</td><td>30021623113</td><td>2024-01-29T02:41:46.904385716UTC</td></tr><tr><td>35.185.161.147:26657</td><td>likecoin-mainnet-2</td><td>Oursky 🔴</td><td>12862814</td><td>8394252</td><td>False</td><td>on</td><td>29562431785</td><td>2024-01-29T02:41:45.021287210UTC</td></tr><tr><td>207.180.238.137:26657</td><td>likecoin-mainnet-2</td><td>moonbeam-RPC 🟢</td><td>12862809</td><td>9234583</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T02:41:12.844261659UTC</td></tr><tr><td>157.230.252.47:26657</td><td>likecoin-mainnet-2</td><td>NTUTBlockchain 🔴</td><td>12862811</td><td>9318400</td><td>False</td><td>on</td><td>890073071</td><td>2024-01-29T02:41:28.858217670UTC</td></tr><tr><td>45.33.97.75:26657</td><td>likecoin-mainnet-2</td><td>CoderNoah 🔴</td><td>12862814</td><td>11014944</td><td>False</td><td>on</td><td>19654684538</td><td>2024-01-29T02:41:43.932233002UTC</td></tr><tr><td>66.45.246.166:1007</td><td>likecoin-mainnet-2</td><td>STAVR-Service 🟢</td><td>12862811</td><td>11931594</td><td>False</td><td>on</td><td>0</td><td>2024-01-29T02:41:34.758269848UTC</td></tr><tr><td>207.180.197.26:26657</td><td>likecoin-mainnet-2</td><td>SupportHK 🔴</td><td>12862808</td><td>12089921</td><td>False</td><td>on</td><td>8798287053</td><td>2024-01-29T02:41:09.649488232UTC</td></tr><tr><td>154.12.227.117:26657</td><td>likecoin-mainnet-2</td><td>50%Banana 🔴</td><td>12862808</td><td>12611811</td><td>False</td><td>on</td><td>772080296</td><td>2024-01-29T02:41:12.446220678UTC</td></tr><tr><td>78.150.106.72:26657</td><td>likecoin-mainnet-2</td><td>kamkcir 🔴</td><td>12862817</td><td>12655255</td><td>False</td><td>on</td><td>283620787</td><td>2024-01-29T02:42:04.425199751UTC</td></tr><tr><td>172.105.153.187:26657</td><td>likecoin-mainnet-2</td><td>mn 🔴</td><td>12862817</td><td>12683911</td><td>False</td><td>off</td><td>29477463187</td><td>2024-01-29T02:42:02.028419460UTC</td></tr><tr><td>165.232.173.74:26657</td><td>likecoin-mainnet-2</td><td>leafwind 🔴</td><td>12862814</td><td>12832281</td><td>False</td><td>off</td><td>48097024848</td><td>2024-01-29T02:41:43.267217665UTC</td></tr><tr><td>167.99.71.225:26657</td><td>likecoin-mainnet-2</td><td>liker_mxp_v2 🔴</td><td>12862818</td><td>12858837</td><td>False</td><td>off</td><td>26687407461</td><td>2024-01-29T02:42:09.521077814UTC</td></tr></table>
