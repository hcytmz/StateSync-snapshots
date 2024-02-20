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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2274237</td><td>1</td><td>False</td><td>off</td><td>294828571879274</td><td>2024-02-19T20:52:26.680954374UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2274237</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-19T20:52:27.489138897UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>2274238</td><td>1</td><td>False</td><td>off</td><td>27067451472639025</td><td>2024-02-19T20:52:37.437209223UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2274239</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-19T20:52:46.676615974UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2274241</td><td>1</td><td>False</td><td>on</td><td>187389752966372</td><td>2024-02-19T20:52:51.460900340UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2274239</td><td>660001</td><td>False</td><td>on</td><td>155890338702520</td><td>2024-02-19T20:52:39.789040375UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>2274237</td><td>962001</td><td>False</td><td>on</td><td>333772381865705</td><td>2024-02-19T20:52:29.907103204UTC</td></tr><tr><td>89.117.63.35:14257</td><td>entangle_33133-1</td><td>VTB-ENTANGLE 🟢</td><td>2274238</td><td>1162001</td><td>False</td><td>off</td><td>0</td><td>2024-02-19T20:52:34.702554773UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2274237</td><td>1312001</td><td>False</td><td>off</td><td>511129254058967</td><td>2024-02-19T20:52:27.152991523UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>2274237</td><td>1910001</td><td>False</td><td>off</td><td>316730524074424</td><td>2024-02-19T20:52:30.237076562UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>2274241</td><td>2042001</td><td>False</td><td>on</td><td>43255829729723701</td><td>2024-02-19T20:52:51.139259404UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2274237</td><td>2049001</td><td>False</td><td>off</td><td>19445177053143</td><td>2024-02-19T20:52:26.257257440UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>2274238</td><td>2098001</td><td>False</td><td>on</td><td>498358550072519</td><td>2024-02-19T20:52:37.170669599UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2274239</td><td>2174239</td><td>False</td><td>off</td><td>46591264469803308</td><td>2024-02-19T20:52:44.238528408UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2274237</td><td>2272001</td><td>False</td><td>on</td><td>0</td><td>2024-02-19T20:52:25.809616111UTC</td></tr></table>
