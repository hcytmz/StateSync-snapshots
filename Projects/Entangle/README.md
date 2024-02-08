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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2077706</td><td>1</td><td>False</td><td>off</td><td>281784076765325</td><td>2024-02-08T03:05:17.035262130UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2077707</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T03:05:17.831383992UTC</td></tr><tr><td>34.118.4.252:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2077707</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T03:05:18.201853285UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>2077709</td><td>1</td><td>False</td><td>off</td><td>27053624834804497</td><td>2024-02-08T03:05:29.707145762UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2077711</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T03:05:34.646133249UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🟢</td><td>2077712</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T03:05:39.787691700UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2077709</td><td>660001</td><td>False</td><td>on</td><td>124563997536521</td><td>2024-02-08T03:05:29.943836238UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2077706</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T03:05:14.283133772UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>2077707</td><td>962001</td><td>False</td><td>on</td><td>324325665506279</td><td>2024-02-08T03:05:20.576847729UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2077706</td><td>1312001</td><td>False</td><td>off</td><td>469415790752137</td><td>2024-02-08T03:05:17.466797847UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>2077707</td><td>1910001</td><td>False</td><td>off</td><td>304925654935508</td><td>2024-02-08T03:05:20.912739674UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>2077709</td><td>1958001</td><td>False</td><td>on</td><td>478741378712927</td><td>2024-02-08T03:05:29.475243372UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2077710</td><td>1977710</td><td>False</td><td>off</td><td>46578755949975824</td><td>2024-02-08T03:05:32.235690206UTC</td></tr><tr><td>158.220.91.214:17157</td><td>entangle_33133-1</td><td>Iryna2 🔴</td><td>2077711</td><td>2042001</td><td>False</td><td>on</td><td>311751469338918</td><td>2024-02-08T03:05:35.138434299UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>2077712</td><td>2042001</td><td>False</td><td>on</td><td>43245390300359479</td><td>2024-02-08T03:05:39.487818091UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2077706</td><td>2049001</td><td>False</td><td>off</td><td>9768054823368</td><td>2024-02-08T03:05:14.655364688UTC</td></tr></table>
