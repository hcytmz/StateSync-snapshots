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




<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>78.46.83.78:26657</td><td>cheqd-mainnet-1</td><td>cstp-cheqd 🔴</td><td>11523018</td><td>1</td><td>False</td><td>on</td><td>2365166134</td><td>2024-01-13T02:18:59.871257601UTC</td></tr><tr><td>13.59.81.97:26657</td><td>cheqd-mainnet-1</td><td>ydp1-chqd 🔴</td><td>11523020</td><td>1</td><td>False</td><td>on</td><td>37717329302</td><td>2024-01-13T02:19:09.997105880UTC</td></tr><tr><td>167.235.133.235:26657</td><td>cheqd-mainnet-1</td><td>danubetech-v2 🔴</td><td>11523022</td><td>1</td><td>False</td><td>on</td><td>13292099545</td><td>2024-01-13T02:19:23.045040832UTC</td></tr><tr><td>208.77.197.82:33657</td><td>cheqd-mainnet-1</td><td>vidulum.app 🟢</td><td>11523029</td><td>8384004</td><td>False</td><td>on</td><td>0</td><td>2024-01-13T02:20:06.431150487UTC</td></tr><tr><td>135.181.6.249:26657</td><td>cheqd-mainnet-1</td><td>verio-id 🟢</td><td>9196500</td><td>8896499</td><td>False</td><td>on</td><td>0</td><td>2024-01-13T02:19:00.218216542UTC</td></tr><tr><td>149.102.137.113:26657</td><td>cheqd-mainnet-1</td><td>node101 🔴</td><td>11523026</td><td>10276869</td><td>False</td><td>on</td><td>7245006964</td><td>2024-01-13T02:19:49.769194544UTC</td></tr><tr><td>80.39.181.74:30657</td><td>cheqd-mainnet-1</td><td>Validavia 🔴</td><td>11523022</td><td>10423019</td><td>False</td><td>on</td><td>2288717576</td><td>2024-01-13T02:19:23.584525446UTC</td></tr><tr><td>142.132.248.253:22257</td><td>cheqd-mainnet-1</td><td>Blackhox 🔴</td><td>11523028</td><td>10538869</td><td>False</td><td>on</td><td>2242371499</td><td>2024-01-13T02:19:56.862305638UTC</td></tr><tr><td>206.189.247.12:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11523019</td><td>11273019</td><td>False</td><td>on</td><td>40635450326</td><td>2024-01-13T02:19:06.752728555UTC</td></tr><tr><td>134.209.190.126:26657</td><td>cheqd-mainnet-1</td><td>seerbytes 🔴</td><td>11523022</td><td>11273022</td><td>False</td><td>on</td><td>222001984</td><td>2024-01-13T02:19:22.791381273UTC</td></tr><tr><td>51.145.165.17:26657</td><td>cheqd-mainnet-1</td><td>DIDLab 🔴</td><td>11523023</td><td>11273023</td><td>False</td><td>on</td><td>20123846232</td><td>2024-01-13T02:19:29.994816946UTC</td></tr><tr><td>13.244.233.116:26657</td><td>cheqd-mainnet-1</td><td>DIDx 🔴</td><td>11523023</td><td>11273023</td><td>False</td><td>on</td><td>3710352823</td><td>2024-01-13T02:19:30.931833053UTC</td></tr><tr><td>159.69.174.238:26657</td><td>cheqd-mainnet-1</td><td>node0-monokee 🔴</td><td>11523024</td><td>11273024</td><td>False</td><td>on</td><td>15711410032</td><td>2024-01-13T02:19:33.296712550UTC</td></tr><tr><td>143.110.218.56:26657</td><td>cheqd-mainnet-1</td><td>continuumloop-mn 🔴</td><td>11523024</td><td>11273024</td><td>False</td><td>on</td><td>6341236720</td><td>2024-01-13T02:19:34.458237603UTC</td></tr><tr><td>206.189.25.194:26657</td><td>cheqd-mainnet-1</td><td>baby-yoda-node 🔴</td><td>11523026</td><td>11273026</td><td>False</td><td>on</td><td>40635450326</td><td>2024-01-13T02:19:47.171387014UTC</td></tr><tr><td>51.159.165.38:26657</td><td>cheqd-mainnet-1</td><td>cheqd-validator-temp 🔴</td><td>11523029</td><td>11446869</td><td>False</td><td>on</td><td>10404439860</td><td>2024-01-13T02:20:03.398783725UTC</td></tr><tr><td>66.45.246.166:26337</td><td>cheqd-mainnet-1</td><td>Paradigm 🔴</td><td>11523027</td><td>11505869</td><td>False</td><td>on</td><td>206321</td><td>2024-01-13T02:19:52.383503213UTC</td></tr><tr><td>135.181.210.171:26337</td><td>cheqd-mainnet-1</td><td>STAVR-Service 🟢</td><td>11523019</td><td>11512869</td><td>False</td><td>on</td><td>0</td><td>2024-01-13T02:19:07.218262573UTC</td></tr></table>
