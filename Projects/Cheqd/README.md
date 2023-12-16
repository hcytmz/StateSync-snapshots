<h1 align="center"> 🔥CHEQD🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Cheqd)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://cheqd.rpc.m.stavr.tech:26337
SEEDS=46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016
cp $HOME/.cheqdnode/data/priv_validator_state.json $HOME/.cheqdnode/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.cheqdnode/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.cheqdnode/config/config.toml
cheqd-noded tendermint unsafe-reset-all --home $HOME/.cheqdnode --keep-addr-book
mv $HOME/.cheqdnode/priv_validator_state.json.backup $HOME/.cheqdnode/data/priv_validator_state.json
sudo systemctl restart cheqd-noded && journalctl -u cheqd-noded -f -o cat
```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop cheqd-noded
cp $HOME/.cheqdnode/data/priv_validator_state.json $HOME/.cheqdnode/priv_validator_state.json.backup
rm -rf $HOME/.cheqdnode/data
curl -o - -L http://cheqd.snapshot.stavr.tech:4/cheqd/cheqd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.cheqdnode --strip-components 2
mv $HOME/.cheqdnode/priv_validator_state.json.backup $HOME/.cheqdnode/data/priv_validator_state.json
wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"
sudo systemctl restart cheqd-noded && journalctl -u cheqd-noded -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Cheqd-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://cheqd.api.m.stavr.tech \
🔥RPC🔥:          http://cheqd.rpc.m.stavr.tech:26337              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://cheqd.grpc.m.stavr.tech:9337 \
🔥peer🔥:         `46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016` \
🔥Addrbook🔥:  `wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.cheqdnode/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/genesis.json"` \
🔥Auto_install script🔥:`wget -O cheqdm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/cheqdm && chmod +x cheqdm && ./cheqdm`

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

[raw Mainnet json](https://rpc-check.cheqdm.stavr.tech/cheqdm/rpc-cheqdm-result.json)
=




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>78.46.83.78:26657</td><td>cheqd-mainnet-1</td><td>cstp-cheqd 🔴</td><td>11122431</td><td>1</td><td>False</td><td>on</td><td>2344526334</td><td>2023-12-16T16:30:36.225561478UTC</td></tr><tr><td>13.59.81.97:26657</td><td>cheqd-mainnet-1</td><td>ydp1-chqd 🔴</td><td>11122432</td><td>1</td><td>False</td><td>on</td><td>35477201888</td><td>2023-12-16T16:30:46.255299376UTC</td></tr><tr><td>167.235.133.235:26657</td><td>cheqd-mainnet-1</td><td>danubetech-v2 🔴</td><td>11122434</td><td>1</td><td>False</td><td>on</td><td>10292099545</td><td>2023-12-16T16:31:00.190775514UTC</td></tr><tr><td>158.220.102.32:26657</td><td>cheqd-mainnet-1</td><td>vmi1259816.contaboserver.net 🟢</td><td>11122442</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T16:31:45.968177319UTC</td></tr><tr><td>75.119.159.96:26657</td><td>cheqd-mainnet-1</td><td>vaipoa.node 🔴</td><td>11122442</td><td>1</td><td>False</td><td>on</td><td>23365856225</td><td>2023-12-16T16:31:46.305633516UTC</td></tr><tr><td>208.77.197.82:33657</td><td>cheqd-mainnet-1</td><td>vidulum.app 🟢</td><td>11122441</td><td>8384004</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T16:31:41.555564111UTC</td></tr><tr><td>135.181.6.249:26657</td><td>cheqd-mainnet-1</td><td>verio-id 🟢</td><td>9196500</td><td>8896499</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T16:30:36.592270408UTC</td></tr><tr><td>65.21.20.218:26657</td><td>cheqd-mainnet-1</td><td>Blockval_Node 🟢</td><td>11122436</td><td>9634953</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T16:31:11.858512886UTC</td></tr><tr><td>149.102.137.113:26657</td><td>cheqd-mainnet-1</td><td>node101 🔴</td><td>11122438</td><td>10276869</td><td>False</td><td>on</td><td>7229458600</td><td>2023-12-16T16:31:25.529508955UTC</td></tr><tr><td>80.39.181.74:30657</td><td>cheqd-mainnet-1</td><td>Validavia 🔴</td><td>11122434</td><td>10423019</td><td>False</td><td>on</td><td>2286501777</td><td>2023-12-16T16:31:02.741175508UTC</td></tr><tr><td>142.132.248.253:22257</td><td>cheqd-mainnet-1</td><td>Blackhox 🔴</td><td>11122440</td><td>10538869</td><td>False</td><td>on</td><td>2226714422</td><td>2023-12-16T16:31:34.529314004UTC</td></tr><tr><td>206.189.247.12:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11122432</td><td>10872432</td><td>False</td><td>on</td><td>40573471843</td><td>2023-12-16T16:30:43.177536425UTC</td></tr><tr><td>13.245.249.96:26657</td><td>cheqd-mainnet-1</td><td>DIDx 🔴</td><td>11122433</td><td>10872433</td><td>False</td><td>on</td><td>3728552430</td><td>2023-12-16T16:30:55.333850799UTC</td></tr><tr><td>134.209.190.126:26657</td><td>cheqd-mainnet-1</td><td>seerbytes 🔴</td><td>11122434</td><td>10872434</td><td>False</td><td>on</td><td>224078286</td><td>2023-12-16T16:30:59.780944033UTC</td></tr><tr><td>51.145.165.17:26657</td><td>cheqd-mainnet-1</td><td>DIDLab 🔴</td><td>11122436</td><td>10872436</td><td>False</td><td>on</td><td>19119257287</td><td>2023-12-16T16:31:09.155805419UTC</td></tr><tr><td>159.69.174.238:26657</td><td>cheqd-mainnet-1</td><td>node0-monokee 🔴</td><td>11122436</td><td>10872436</td><td>False</td><td>on</td><td>14718138542</td><td>2023-12-16T16:31:11.539164008UTC</td></tr><tr><td>143.110.218.56:26657</td><td>cheqd-mainnet-1</td><td>continuumloop-mn 🔴</td><td>11122436</td><td>10872436</td><td>False</td><td>on</td><td>6655452218</td><td>2023-12-16T16:31:12.632474499UTC</td></tr><tr><td>206.189.25.194:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11122438</td><td>10872438</td><td>False</td><td>on</td><td>40573471843</td><td>2023-12-16T16:31:23.182393818UTC</td></tr><tr><td>66.45.246.166:26337</td><td>cheqd-mainnet-1</td><td>Paradigm 🔴</td><td>11122439</td><td>10979869</td><td>False</td><td>on</td><td>1</td><td>2023-12-16T16:31:28.152842435UTC</td></tr><tr><td>135.181.210.171:26337</td><td>cheqd-mainnet-1</td><td>STAVR-Service 🟢</td><td>11122432</td><td>11110869</td><td>False</td><td>on</td><td>0</td><td>2023-12-16T16:30:43.520423831UTC</td></tr></table>