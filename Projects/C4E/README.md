<h1 align="center"> 🔥C4E🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/C4E)
=

<h1 align="center"> MAINNET</h1>

# StateSync C4E Mainnet
```python
SNAP_RPC=http://c4e.rpc.m.stavr.tech:17097
peers="5ed0b8f7989d34438f71ccc74b0ab0fbf763a475@c4e.peer.stavr.tech:17096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.c4e-chain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.c4e-chain/config/config.toml
c4ed tendermint unsafe-reset-all --home /root/.c4e-chain --keep-addr-book
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop c4ed
cp $HOME/.c4e-chain/data/priv_validator_state.json $HOME/.c4e-chain/priv_validator_state.json.backup
rm -rf $HOME/.c4e-chain/data
curl -o - -L http://c4e.snapshot.stavr.tech:1018/c4e/c4e-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.c4e-chain --strip-components 2
mv $HOME/.c4e-chain/priv_validator_state.json.backup $HOME/.c4e-chain/data/priv_validator_state.json
wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/addrbook.json"
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER MAINNET🔥:  https://explorer.stavr.tech/C4E/staking            `Indexer "ON"` \
🔥EXPLORER TESTET🔥:   https://explorer.stavr.tech/C4E-Testnet/staking     `Indexer "ON"` \
🔥API MAINNET🔥:       https://c4e.api.m.stavr.tech \
🔥API TESTNET🔥:       https://c4e.api.t.stavr.tech \
🔥RPC🔥:               http://c4e.rpc.m.stavr.tech:17097                  `Snapshot-interval = 100` \
🔥gRPC🔥:              http://c4e.grpc.m.stavr.tech:7029 \
🔥peer🔥:              `5ed0b8f7989d34438f71ccc74b0ab0fbf763a475@c4e.peer.stavr.tech:17096` \
🔥Addrbook🔥:    ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/genesis.json -O $HOME/.c4e-chain/config/genesis.json``` \
🔥Auto_install script🔥: ```wget -O c4 https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/c4 && chmod +x c4 && ./c4```





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

[raw json](https://rpc-check.c4e.stavr.tech/c4e/rpc-c4e-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.21.129.95:36657</td><td>perun-1</td><td>cyberG 🟢</td><td>6094694</td><td>0</td><td>False</td><td>0</td><td>2023-12-01T08:38:24.600990584UTC</td></tr><tr><td>79.137.68.96:26657</td><td>perun-1</td><td>archive-node2 🟢</td><td>6094691</td><td>1</td><td>False</td><td>0</td><td>2023-12-01T08:38:07.633518866UTC</td></tr><tr><td>65.108.70.119:33657</td><td>perun-1</td><td>AlxVoy 🟢</td><td>6094694</td><td>1</td><td>False</td><td>0</td><td>2023-12-01T08:38:24.216777554UTC</td></tr><tr><td>149.202.66.111:26657</td><td>perun-1</td><td>archive-node1 🟢</td><td>6094696</td><td>1</td><td>False</td><td>0</td><td>2023-12-01T08:38:41.140751145UTC</td></tr><tr><td>185.245.182.192:46657</td><td>perun-1</td><td>Meerlabs 🔴</td><td>6094697</td><td>1051501</td><td>False</td><td>493550</td><td>2023-12-01T08:38:46.771916581UTC</td></tr><tr><td>185.215.167.18:26657</td><td>perun-1</td><td>Rawalot 🔴</td><td>6094700</td><td>1090501</td><td>False</td><td>579034</td><td>2023-12-01T08:38:59.105217310UTC</td></tr><tr><td>95.70.184.178:44657</td><td>perun-1</td><td>mahof 🔴</td><td>6094693</td><td>2342001</td><td>False</td><td>1357006</td><td>2023-12-01T08:38:23.519665018UTC</td></tr><tr><td>209.182.239.169:46657</td><td>perun-1</td><td>SECARD 🔴</td><td>6094696</td><td>2616101</td><td>False</td><td>675729</td><td>2023-12-01T08:38:38.460473431UTC</td></tr><tr><td>89.117.58.109:26657</td><td>perun-1</td><td>medes 🔴</td><td>6094699</td><td>2826001</td><td>False</td><td>471345</td><td>2023-12-01T08:38:53.857618894UTC</td></tr><tr><td>5.135.141.191:26657</td><td>perun-1</td><td>c4e-sentry1-mainnet 🟢</td><td>6094691</td><td>4267001</td><td>False</td><td>0</td><td>2023-12-01T08:38:07.212678730UTC</td></tr><tr><td>65.109.30.185:26657</td><td>perun-1</td><td>c4e-sentry2-mainnet 🟢</td><td>6094697</td><td>5186001</td><td>False</td><td>0</td><td>2023-12-01T08:38:46.467644967UTC</td></tr><tr><td>77.55.216.80:26657</td><td>perun-1</td><td>c4e-sentry4-mainnet 🟢</td><td>6094693</td><td>5187001</td><td>False</td><td>0</td><td>2023-12-01T08:38:23.889471117UTC</td></tr><tr><td>65.108.75.107:39657</td><td>perun-1</td><td>node 🟢</td><td>6094694</td><td>5198801</td><td>False</td><td>0</td><td>2023-12-01T08:38:27.377216112UTC</td></tr><tr><td>163.172.18.144:26657</td><td>perun-1</td><td>c4e-sentry3-mainnet 🟢</td><td>6094698</td><td>5286001</td><td>False</td><td>0</td><td>2023-12-01T08:38:47.411873305UTC</td></tr><tr><td>65.108.141.109:39657</td><td>perun-1</td><td>node 🟢</td><td>6094691</td><td>5303301</td><td>False</td><td>0</td><td>2023-12-01T08:38:10.102662895UTC</td></tr><tr><td>135.181.114.86:30657</td><td>perun-1</td><td>NodeName 🔴</td><td>6094697</td><td>5508301</td><td>False</td><td>333717</td><td>2023-12-01T08:38:41.541691234UTC</td></tr><tr><td>65.108.125.55:16557</td><td>perun-1</td><td>Validatrium-rpc 🟢</td><td>6094699</td><td>5551301</td><td>False</td><td>0</td><td>2023-12-01T08:38:56.310867693UTC</td></tr><tr><td>185.252.235.83:26657</td><td>perun-1</td><td>Alien 🔴</td><td>6094697</td><td>5736001</td><td>False</td><td>380508</td><td>2023-12-01T08:38:41.958290597UTC</td></tr><tr><td>38.242.220.64:16657</td><td>perun-1</td><td>mahof 🟢</td><td>6094696</td><td>5980001</td><td>False</td><td>0</td><td>2023-12-01T08:38:38.759156912UTC</td></tr><tr><td>65.108.66.174:30657</td><td>perun-1</td><td>hello-BccNodesRPC 🟢</td><td>6094694</td><td>5985401</td><td>False</td><td>0</td><td>2023-12-01T08:38:24.994392179UTC</td></tr><tr><td>168.119.226.107:26957</td><td>perun-1</td><td>c4e_rpc 🟢</td><td>6094692</td><td>5994692</td><td>False</td><td>0</td><td>2023-12-01T08:38:16.493750331UTC</td></tr><tr><td>65.108.124.219:31657</td><td>perun-1</td><td>MantiCore 🔴</td><td>6094693</td><td>5994693</td><td>False</td><td>837444</td><td>2023-12-01T08:38:23.130216626UTC</td></tr><tr><td>135.181.133.249:13457</td><td>perun-1</td><td>StakeUp 🔴</td><td>6094689</td><td>6015001</td><td>False</td><td>1357007</td><td>2023-12-01T08:37:58.601271290UTC</td></tr><tr><td>135.181.210.171:17097</td><td>perun-1</td><td>STAVR-Service 🟢</td><td>6094695</td><td>6094101</td><td>False</td><td>0</td><td>2023-12-01T08:38:29.882654501UTC</td></tr></table>
