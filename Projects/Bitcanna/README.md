<h1 align="center"> 🔥BITCANNA MAINNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Bitcanna)
=

# StateSync
```python
RPC="https://bitcanna.rpc.m.stavr.tech:443"
peers="644ac886e7f2fe082b3556dc694076e71a4e959a@bitcanna.peers.stavr.tech:21326"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.bcna/config/config.toml
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.bcna/config/config.toml
sudo systemctl stop bcnad && bcnad tendermint unsafe-reset-all --keep-addr-book
sudo systemctl restart bcnad && sudo journalctl -u bcnad -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
snap install lz4
sudo systemctl stop bcnad
cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup
rm -rf $HOME/.bcna/data
curl -o - -L http://bitcanna.snapshot.stavr.tech:1004/bca/bca-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.bcna --strip-components 2
mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json
wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/addrbook.json"
sudo systemctl restart bcnad && journalctl -u bcnad -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:    https://explorer.stavr.tech/Bitcanna/staking          `Indexer "ON"` \
🔥EXPLORER Devnet🔥:     https://explorer.stavr.tech/Bitcanna-DEV/staking     `Indexer "ON"` \
🔥API Mainnet🔥:         https://bitcanna.api.m.stavr.tech \
🔥API Devnet🔥:          https://bitcanna.api.dev.stavr.tech \
🔥RPC Mainnet🔥:         https://bitcanna.rpc.m.stavr.tech:443         `Snapshot-interval = 300` \
🔥gRPC Mainnet🔥:        http://bitcanna.grpc.m.stavr.tech:9081 \
🔥gRPC Devnet🔥:         http://bitcanna.grpc.dev.stavr.tech:2901 \
🔥peer Mainnet🔥:        `644ac886e7f2fe082b3556dc694076e71a4e959a@bitcanna.peers.stavr.tech:21326` \
🔥peer Devnet🔥:         `b0c7e5c69aaf00626baaf7c59370029b587a91a4@bitcannadev.peers.stavr.tech:30006` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/addrbook.json"``` \
🔥Addrbook Devnet🔥:    ```wget -O $HOME/.bcna/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/Bitcanna_DEV/addrbook.json"``` \
🔥Auto_install script Mainnet🔥:```wget -O bitcanna https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Bitcanna/bitcanna && chmod +x bitcanna && ./bitcanna```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Bitcanna/Decentralization)🔥
=

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

[raw Mainnet json](https://rpc-check.bcam.stavr.tech/bcam/rpc-bcam-result.json) \
[raw Testnet json](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Bitcanna/Rpc-Check-Testnet)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>149.102.133.38:16657</td><td>bitcanna-1</td><td>second 🟢</td><td>13227277</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:38.054208342UTC</td></tr><tr><td>95.216.242.82:36657</td><td>bitcanna-1</td><td>Moniker 🟢</td><td>13227266</td><td>5776907</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:57:33.420337800UTC</td></tr><tr><td>144.76.97.251:27657</td><td>bitcanna-1</td><td>AlxVoy 🟢</td><td>13227275</td><td>8805201</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:27.531140872UTC</td></tr><tr><td>65.109.155.238:33657</td><td>bitcanna-1</td><td>MultVR 🔴</td><td>13227271</td><td>9933415</td><td>False</td><td>on</td><td>353129</td><td>2024-03-29T11:58:05.534335860UTC</td></tr><tr><td>167.235.9.223:61157</td><td>bitcanna-1</td><td>F5Nodes 🔴</td><td>13227272</td><td>12084001</td><td>False</td><td>on</td><td>573</td><td>2024-03-29T11:58:09.830394877UTC</td></tr><tr><td>65.109.93.152:26357</td><td>bitcanna-1</td><td>AlxVoy 🔴</td><td>13227277</td><td>12109301</td><td>False</td><td>on</td><td>1391954</td><td>2024-03-29T11:58:38.561752382UTC</td></tr><tr><td>161.97.150.65:26657</td><td>bitcanna-1</td><td>New_peer 🟢</td><td>13227270</td><td>12254001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:57:58.302204568UTC</td></tr><tr><td>208.77.197.82:31657</td><td>bitcanna-1</td><td>vidulum.app 🟢</td><td>13227271</td><td>12386934</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:01.093267330UTC</td></tr><tr><td>193.34.144.156:26657</td><td>bitcanna-1</td><td>Paranorm 🟢</td><td>13227273</td><td>13042501</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:14.474727941UTC</td></tr><tr><td>65.108.131.190:21957</td><td>bitcanna-1</td><td>bitcanna 🔴</td><td>13227273</td><td>13127273</td><td>False</td><td>on</td><td>420338</td><td>2024-03-29T11:58:14.235546013UTC</td></tr><tr><td>104.207.129.116:26657</td><td>bitcanna-1</td><td>Sentry1-ValidatorNode 🟢</td><td>13227277</td><td>13128001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:39.237311987UTC</td></tr><tr><td>144.91.65.13:26667</td><td>bitcanna-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>13227274</td><td>13219001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:22.945615743UTC</td></tr><tr><td>135.181.210.171:21327</td><td>bitcanna-1</td><td>STAVR-Service 🟢</td><td>13227275</td><td>13224001</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T11:58:27.317689838UTC</td></tr></table>
