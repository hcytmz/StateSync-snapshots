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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>34.66.248.218:26657</td><td>likecoin-mainnet-2</td><td>dataxStaking 🔴</td><td>13527652</td><td>1</td><td>False</td><td>on</td><td>21817695910</td><td>2024-03-14T21:48:41.341879012UTC</td></tr><tr><td>154.53.63.22:26657</td><td>likecoin-mainnet-2</td><td>martianforest 🔴</td><td>13527655</td><td>1</td><td>False</td><td>on</td><td>671130449</td><td>2024-03-14T21:48:59.459702147UTC</td></tr><tr><td>144.126.131.195:26657</td><td>likecoin-mainnet-2</td><td>WeLike 🔴</td><td>13527651</td><td>5101130</td><td>False</td><td>on</td><td>115880133924</td><td>2024-03-14T21:48:34.573117014UTC</td></tr><tr><td>188.166.226.230:26657</td><td>likecoin-mainnet-2</td><td>PM 🔴</td><td>13527655</td><td>7730955</td><td>False</td><td>on</td><td>24821000113</td><td>2024-03-14T21:49:01.014339374UTC</td></tr><tr><td>207.180.238.137:26657</td><td>likecoin-mainnet-2</td><td>moonbeam-RPC 🟢</td><td>13527651</td><td>9234583</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T21:48:31.826629122UTC</td></tr><tr><td>207.180.197.26:26657</td><td>likecoin-mainnet-2</td><td>SupportHK 🔴</td><td>13527650</td><td>12089921</td><td>False</td><td>on</td><td>8671686641</td><td>2024-03-14T21:48:26.790227058UTC</td></tr><tr><td>154.12.227.117:26657</td><td>likecoin-mainnet-2</td><td>50%Banana 🔴</td><td>13527650</td><td>12611811</td><td>False</td><td>on</td><td>751034009</td><td>2024-03-14T21:48:31.556660865UTC</td></tr><tr><td>78.150.105.172:26657</td><td>likecoin-mainnet-2</td><td>kamkcir 🔴</td><td>13527654</td><td>12655255</td><td>False</td><td>on</td><td>416852848</td><td>2024-03-14T21:48:51.541463432UTC</td></tr><tr><td>172.105.153.187:26657</td><td>likecoin-mainnet-2</td><td>mn 🔴</td><td>13527658</td><td>12683911</td><td>False</td><td>off</td><td>29100049598</td><td>2024-03-14T21:49:15.951769045UTC</td></tr><tr><td>45.33.97.75:26657</td><td>likecoin-mainnet-2</td><td>CoderNoah 🔴</td><td>13527655</td><td>12741110</td><td>False</td><td>on</td><td>19324540279</td><td>2024-03-14T21:48:57.543696121UTC</td></tr><tr><td>35.185.161.147:26657</td><td>likecoin-mainnet-2</td><td>Oursky 🔴</td><td>13527655</td><td>12887155</td><td>False</td><td>on</td><td>28516165361</td><td>2024-03-14T21:48:58.558359703UTC</td></tr><tr><td>66.45.246.166:1007</td><td>likecoin-mainnet-2</td><td>STAVR-Service 🟢</td><td>13527653</td><td>13292630</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T21:48:48.576394232UTC</td></tr><tr><td>165.22.106.32:26657</td><td>likecoin-mainnet-2</td><td>Liker.Social 🔴</td><td>13527654</td><td>13405629</td><td>False</td><td>on</td><td>48530469606</td><td>2024-03-14T21:48:53.088285101UTC</td></tr><tr><td>165.232.173.74:26657</td><td>likecoin-mainnet-2</td><td>leafwind 🔴</td><td>13527655</td><td>13441800</td><td>False</td><td>off</td><td>42480222919</td><td>2024-03-14T21:48:56.904001241UTC</td></tr><tr><td>167.99.71.225:26657</td><td>likecoin-mainnet-2</td><td>liker_mxp_v2 🔴</td><td>13527660</td><td>13526606</td><td>False</td><td>off</td><td>26775045546</td><td>2024-03-14T21:49:25.623691666UTC</td></tr></table>
