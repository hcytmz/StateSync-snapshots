<h1 align="center"> 🔥CHEQD🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Cheqd)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://cheqd.rpc.m.stavr.tech:443
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
🔥RPC🔥:          https://cheqd.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://cheqd.grpc.m.stavr.tech:9337 \
🔥peer🔥:         `46bb1e68fcc2750ecdc4253986d653f4bd7228ef@cheqd.peer.stavr.tech:21016` \
🔥Addrbook🔥:  `wget -O $HOME/.cheqdnode/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.cheqdnode/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/genesis.json"` \
🔥Auto_install script🔥:`wget -O cheqdm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cheqd/cheqdm && chmod +x cheqdm && ./cheqdm` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Cheqd/Decentralization)🔥

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




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>78.46.83.78:26657</td><td>cheqd-mainnet-1</td><td>cstp-cheqd 🔴</td><td>11846746</td><td>1</td><td>False</td><td>on</td><td>2374641697</td><td>2024-02-04T06:54:14.701675556UTC</td></tr><tr><td>13.59.81.97:26657</td><td>cheqd-mainnet-1</td><td>ydp1-chqd 🔴</td><td>11846751</td><td>1</td><td>False</td><td>on</td><td>38227788855</td><td>2024-02-04T06:54:45.404419812UTC</td></tr><tr><td>167.235.133.235:26657</td><td>cheqd-mainnet-1</td><td>danubetech-v2 🔴</td><td>11846757</td><td>1</td><td>False</td><td>on</td><td>13297099545</td><td>2024-02-04T06:55:20.575569976UTC</td></tr><tr><td>158.220.102.32:26657</td><td>cheqd-mainnet-1</td><td>vmi1259816.contaboserver.net 🟢</td><td>11846785</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T06:57:59.528466391UTC</td></tr><tr><td>208.77.197.82:33657</td><td>cheqd-mainnet-1</td><td>vidulum.app 🟢</td><td>11846782</td><td>8384004</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T06:57:44.701096806UTC</td></tr><tr><td>135.181.6.249:26657</td><td>cheqd-mainnet-1</td><td>verio-id 🟢</td><td>9196500</td><td>8896499</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T06:54:21.186647189UTC</td></tr><tr><td>149.102.137.113:26657</td><td>cheqd-mainnet-1</td><td>node101 🔴</td><td>11846771</td><td>10276869</td><td>False</td><td>on</td><td>7249092474</td><td>2024-02-04T06:56:42.301196430UTC</td></tr><tr><td>142.132.248.253:22257</td><td>cheqd-mainnet-1</td><td>Blackhox 🔴</td><td>11846777</td><td>10538869</td><td>False</td><td>on</td><td>2267472541</td><td>2024-02-04T06:57:16.390542133UTC</td></tr><tr><td>65.21.20.218:26657</td><td>cheqd-mainnet-1</td><td>Blockval_Node 🟢</td><td>11846763</td><td>11356095</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T06:55:55.446428542UTC</td></tr><tr><td>51.159.165.38:26657</td><td>cheqd-mainnet-1</td><td>cheqd-validator-temp 🔴</td><td>11846779</td><td>11446869</td><td>False</td><td>on</td><td>10410983361</td><td>2024-02-04T06:57:29.384789332UTC</td></tr><tr><td>66.45.246.166:26337</td><td>cheqd-mainnet-1</td><td>Paradigm 🔴</td><td>11846773</td><td>11505869</td><td>False</td><td>on</td><td>110321</td><td>2024-02-04T06:56:53.411620237UTC</td></tr><tr><td>206.189.247.12:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11846749</td><td>11596749</td><td>False</td><td>on</td><td>40854227210</td><td>2024-02-04T06:54:31.903268467UTC</td></tr><tr><td>51.145.165.17:26657</td><td>cheqd-mainnet-1</td><td>DIDLab 🔴</td><td>11846761</td><td>11596761</td><td>False</td><td>on</td><td>19086302285</td><td>2024-02-04T06:55:41.482556421UTC</td></tr><tr><td>13.244.233.116:26657</td><td>cheqd-mainnet-1</td><td>DIDx 🔴</td><td>11846762</td><td>11596761</td><td>False</td><td>on</td><td>3717477323</td><td>2024-02-04T06:55:44.456294072UTC</td></tr><tr><td>159.69.174.238:26657</td><td>cheqd-mainnet-1</td><td>node0-monokee 🔴</td><td>11846763</td><td>11596763</td><td>False</td><td>on</td><td>15210974643</td><td>2024-02-04T06:55:50.988845993UTC</td></tr><tr><td>143.110.218.56:26657</td><td>cheqd-mainnet-1</td><td>continuumloop-mn 🔴</td><td>11846765</td><td>11596765</td><td>False</td><td>on</td><td>6188549357</td><td>2024-02-04T06:56:02.458832974UTC</td></tr><tr><td>206.189.25.194:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11846770</td><td>11596769</td><td>False</td><td>on</td><td>40854227210</td><td>2024-02-04T06:56:33.727507722UTC</td></tr><tr><td>135.181.210.171:26337</td><td>cheqd-mainnet-1</td><td>STAVR-Service 🟢</td><td>11846749</td><td>11832869</td><td>False</td><td>on</td><td>0</td><td>2024-02-04T06:54:32.329974384UTC</td></tr></table>
