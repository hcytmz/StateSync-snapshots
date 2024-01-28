<h1 align="center"> 🔥Medibloc🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Medibloc)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://panacea.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.panacea/config/config.toml
panacead tendermint unsafe-reset-all
wget -O $HOME/.panacea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Medibloc/addrbook.json"
sudo systemctl restart panacead && sudo journalctl -u panacead -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop panacead
cp $HOME/.panacea/data/priv_validator_state.json $HOME/.panacea/priv_validator_state.json.backup
rm -rf $HOME/.panacea/data
curl -o - -L https://panacea.snapshot.stavr.tech/panacea/panacea-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.panacea --strip-components 2
mv $HOME/.panacea/priv_validator_state.json.backup $HOME/.panacea/data/priv_validator_state.json
wget -O $HOME/.panacea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Medibloc/addrbook.json"
sudo systemctl restart panacead && journalctl -u panacead -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Medibloc-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://med.api.m.stavr.tech \
🔥RPC🔥:          https://panacea.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://panacea.grpc.m.stavr.tech:104 \
🔥seed🔥:      `ff635596139a13cb782de8a4827b0c53463db167@panacea.seed.stavr.tech:2106` \
🔥Addrbook🔥:  `wget -O $HOME/.panacea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Medibloc/addrbook.json"` \
🔥Auto_install script🔥:`wget -O mediblocm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Medibloc/mediblocm && chmod +x mediblocm && ./mediblocm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Medibloc/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.panaceam.stavr.tech/panaceam/rpc-panaceam-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>13.251.23.253:26657</td><td>panacea-3</td><td>mainnet-singapore-archive-p3-b 🟢</td><td>14504486</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T12:47:32.790407149UTC</td></tr><tr><td>3.36.46.111:26657</td><td>panacea-3</td><td>VaccineSwap 🟢</td><td>14504488</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T12:47:43.641584342UTC</td></tr><tr><td>3.35.81.103:26657</td><td>panacea-3</td><td>ip-10-242-1-158.ec2.internal 🟢</td><td>14504492</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T12:48:04.927081130UTC</td></tr><tr><td>65.108.126.22:26697</td><td>panacea-3</td><td>StakeLab 🔴</td><td>14504493</td><td>9427369</td><td>False</td><td>off</td><td>366418</td><td>2024-01-28T12:48:07.994994293UTC</td></tr><tr><td>52.78.1.106:26657</td><td>panacea-3</td><td>admiralYISOONSHIN 🔴</td><td>14504495</td><td>10175001</td><td>False</td><td>on</td><td>85746343</td><td>2024-01-28T12:48:19.993832484UTC</td></tr><tr><td>3.36.50.133:26657</td><td>panacea-3</td><td>mainnet-seoul-sentry 🟢</td><td>14504489</td><td>10643001</td><td>False</td><td>off</td><td>0</td><td>2024-01-28T12:47:47.127163596UTC</td></tr><tr><td>13.124.96.254:26657</td><td>panacea-3</td><td>duplex-b 🟢</td><td>14504490</td><td>10643001</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T12:47:52.685368159UTC</td></tr><tr><td>52.77.227.241:26657</td><td>panacea-3</td><td>mainnet-singapore-sentry 🟢</td><td>14504487</td><td>10644001</td><td>False</td><td>off</td><td>0</td><td>2024-01-28T12:47:36.081051901UTC</td></tr><tr><td>13.114.44.199:26657</td><td>panacea-3</td><td>mainnet-tokyo-sentry 🟢</td><td>14504493</td><td>10644001</td><td>False</td><td>off</td><td>0</td><td>2024-01-28T12:48:06.325895668UTC</td></tr><tr><td>148.251.235.130:16657</td><td>panacea-3</td><td>node-snap 🟢</td><td>14504493</td><td>13520761</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T12:48:08.273360871UTC</td></tr><tr><td>66.45.246.166:2107</td><td>panacea-3</td><td>STAVR-Service 🟢</td><td>14504491</td><td>14504201</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T12:47:59.414842652UTC</td></tr></table>