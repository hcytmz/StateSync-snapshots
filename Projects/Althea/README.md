<h1 align="center"> 🔥Althea🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Althea)
=

<h1 align="center"> MAINNET</h1>

# StateSync Althea Mainnet
```python
SNAP_RPC=https://althea.rpc.m.stavr.tech:443
peers="063fec5334040572f55b06f9ff6284d0f2f01ced@althea.peers.stavr.tech:17886"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.althea/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.althea/config/config.toml
althea tendermint unsafe-reset-all --home /root/.althea
systemctl restart althea && journalctl -u althea -f -o cat
```
# SnapShot updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop althea
cp $HOME/.althea/data/priv_validator_state.json $HOME/.althea/priv_validator_state.json.backup
rm -rf $HOME/.althea/data
curl -o - -L https://althea.snapshot.stavr.tech/althea-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.althea --strip-components 2
mv $HOME/.althea/priv_validator_state.json.backup $HOME/.althea/data/priv_validator_state.json
wget -O $HOME/.althea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/addrbook.json"
sudo systemctl restart althea && journalctl -u althea -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Althea-Mainnet/staking        `Indexer "ON"` \
🔥API🔥:      https://althea.api.m.stavr.tech \
🔥RPC🔥:      https://althea.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:     http://althea.grpc.m.stavr.tech:7219 \
🔥peer🔥:     `063fec5334040572f55b06f9ff6284d0f2f01ced@althea.peers.stavr.tech:17886` \
🔥Genesis🔥: `wget -O $HOME/.althea/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/genesis.json"` \
🔥Addrbook🔥: `wget -O $HOME/.althea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/addrbook.json"` \
🔥Auto_install script🔥:  `wget -O altheam https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/altheam && chmod +x altheam && ./altheam`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Althea/Decentralization)🔥
=

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

[raw json](https://rpc-check.althea.stavr.tech/althea/rpcalthea_result.json)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.181.210.171:17887</td><td>althea_417834-4</td><td>STAVR-Service 🟢</td><td>101369</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-14T13:03:41.788273990UTC</td></tr><tr><td>5.9.106.214:20557</td><td>althea_417834-4</td><td>mzonder 🔴</td><td>101369</td><td>1</td><td>False</td><td>on</td><td>6980</td><td>2024-03-14T13:03:42.035389721UTC</td></tr></table>
