<h1 align="center"> 🔥Dymension🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

<h1 align="center"> TESTNET</h1>

# StateSync Dymension Testnet
```python
SNAP_RPC=https://dym.rpc.t.stavr.tech:443
peers="263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dymension/config/config.toml
dymd tendermint unsafe-reset-all --home /root/.dymension
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Dymension-testnet/staking        `Indexer "ON"` \
🔥API🔥:          https://dymension.api.t.stavr.tech \
🔥RPC🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis🔥:     ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dymension/Decentralization)🔥


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

[raw json](https://rpc-check.dymt.stavr.tech/dymt/rpc-dymt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>2333478</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:31:39.092784972UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:30:21.911122076UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-01-28T23:31:38.242591981UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>2333466</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:30:25.941943217UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>2333469</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:30:46.356838709UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>2333469</td><td>1652923</td><td>False</td><td>off</td><td>3</td><td>2024-01-28T23:30:47.027239534UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>2333475</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:20.403563289UTC</td></tr><tr><td>46.4.99.152:31741</td><td>froopyland_100-1</td><td>node 🟢</td><td>2333475</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:31:22.755987615UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>2333477</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:31.306400015UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>2333479</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T23:31:46.166054586UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>2333472</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:05.259545187UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>2333477</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:31.695981222UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>2333479</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:45.794991107UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>2333466</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:30:26.288600610UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>2333474</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:15.585079116UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>2333475</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T23:31:20.134973936UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🔴</td><td>2333479</td><td>1723012</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:46.544752855UTC</td></tr><tr><td>192.99.160.197:26657</td><td>froopyland_100-1</td><td>NodeName 🟢</td><td>1829304</td><td>1826584</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:31:51.399725741UTC</td></tr><tr><td>194.233.90.134:26657</td><td>froopyland_100-1</td><td>geonodes 🔴</td><td>2333473</td><td>2015001</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:06.317464683UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>2333468</td><td>2033468</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:30:37.834234441UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>2333480</td><td>2060558</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T23:31:51.665088869UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>2333472</td><td>2076584</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:31:04.474958424UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>2333474</td><td>2077398</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T23:31:12.726598585UTC</td></tr><tr><td>167.235.9.223:61557</td><td>froopyland_100-1</td><td>F5Nodes 🔴</td><td>2333470</td><td>2100380</td><td>False</td><td>off</td><td>1</td><td>2024-01-28T23:30:53.599078947UTC</td></tr><tr><td>152.53.16.17:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>2333465</td><td>2169800</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:30:25.094220307UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>2333466</td><td>2225118</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:30:30.800400552UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>2333465</td><td>2266474</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:30:22.583552140UTC</td></tr><tr><td>144.91.65.13:26697</td><td>froopyland_100-1</td><td>AviaDoc_by_AviaOne 🟢</td><td>2333467</td><td>2315718</td><td>False</td><td>on</td><td>0</td><td>2024-01-28T23:30:37.484937388UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>2333472</td><td>2322923</td><td>False</td><td>on</td><td>1</td><td>2024-01-28T23:31:04.868170532UTC</td></tr></table>
