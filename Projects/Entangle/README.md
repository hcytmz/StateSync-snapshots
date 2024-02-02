<h1 align="center"> 🔥Entangle🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Entangle)
=

<h1 align="center"> TESTNET</h1>

# StateSync Entangle Testnet
```python
SOON
```
# SnapShot (~50 GB) Arhive node
```python
cd $HOME
apt install lz4
sudo systemctl stop entangled
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.entangled/config/config.toml
cp $HOME/.entangled/data/priv_validator_state.json $HOME/.entangled/priv_validator_state.json.backup
rm -rf $HOME/.entangled/data
curl -o - -L https://entangle.snapshot.stavr.tech/entagle/entagle-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.entangled --strip-components 2
mv $HOME/.entangled/priv_validator_state.json.backup $HOME/.entangled/data/priv_validator_state.json
wget -O $HOME/.entangled/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Entangle/addrbook.json"
sudo systemctl restart entangled && journalctl -u entangled -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Entangle-testnet/staking        `Indexer "ON"` \
🔥API🔥:      https://entangle.api.t.stavr.tech \
🔥Addrbook🔥: ```wget -O $HOME/.entangled/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Entangle/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O entaglet https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Entangle/entaglet && chmod +x entaglet && ./entaglet`


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

[raw json](https://rpc-check.entangt.stavr.tech/entangt/rpc-entangt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>1982231</td><td>1</td><td>False</td><td>off</td><td>279523470054723</td><td>2024-02-02T14:12:25.071106271UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1982232</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-02T14:12:26.286807884UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1982234</td><td>1</td><td>False</td><td>off</td><td>27051536422893186</td><td>2024-02-02T14:12:40.388076231UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1982235</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-02T14:12:47.422661068UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>1982236</td><td>1</td><td>False</td><td>on</td><td>163402739579782</td><td>2024-02-02T14:12:50.087755886UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>1982235</td><td>660001</td><td>False</td><td>on</td><td>123671365347648</td><td>2024-02-02T14:12:42.733452448UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1982231</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-02-02T14:12:24.670863276UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1982232</td><td>962001</td><td>False</td><td>on</td><td>324046902905202</td><td>2024-02-02T14:12:28.614669147UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1982232</td><td>1312001</td><td>False</td><td>off</td><td>460297573713193</td><td>2024-02-02T14:12:25.546488116UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1982236</td><td>1716001</td><td>False</td><td>on</td><td>43682150326023543</td><td>2024-02-02T14:12:49.750402578UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1982235</td><td>1882235</td><td>False</td><td>off</td><td>46577002386356485</td><td>2024-02-02T14:12:45.059652859UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>1982232</td><td>1910001</td><td>False</td><td>off</td><td>303683804995620</td><td>2024-02-02T14:12:28.976724669UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>1982234</td><td>1958001</td><td>False</td><td>on</td><td>477094729365342</td><td>2024-02-02T14:12:40.130821170UTC</td></tr><tr><td>86.48.0.190:15657</td><td>entangle_33133-1</td><td>vmi1185834.contaboserver.net 🟢</td><td>1977539</td><td>1961001</td><td>False</td><td>off</td><td>0</td><td>2024-02-02T14:12:25.945519771UTC</td></tr><tr><td>212.22.70.9:56657</td><td>entangle_33133-1</td><td>Sr20de 🟢</td><td>1982231</td><td>1971001</td><td>False</td><td>off</td><td>0</td><td>2024-02-02T14:12:24.360670372UTC</td></tr></table>
