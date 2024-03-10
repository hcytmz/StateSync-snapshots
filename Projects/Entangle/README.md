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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2579480</td><td>1</td><td>False</td><td>off</td><td>309555138737431</td><td>2024-03-10T16:04:27.855485188UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2579480</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T16:04:30.545211579UTC</td></tr><tr><td>34.118.4.252:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2579480</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T16:04:30.849099275UTC</td></tr><tr><td>34.77.213.145:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2579480</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T16:04:33.376596119UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2579483</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T16:04:52.987164283UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2579484</td><td>1</td><td>False</td><td>on</td><td>215081779349464</td><td>2024-03-10T16:04:55.577443704UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2579482</td><td>660001</td><td>False</td><td>on</td><td>180849587673254</td><td>2024-03-10T16:04:46.357672765UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2579480</td><td>1312001</td><td>False</td><td>off</td><td>658031979066927</td><td>2024-03-10T16:04:28.171971043UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>2579480</td><td>1910001</td><td>False</td><td>off</td><td>330854491015632</td><td>2024-03-10T16:04:33.128555993UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2579480</td><td>2049001</td><td>False</td><td>off</td><td>29445780867813</td><td>2024-03-10T16:04:25.554843062UTC</td></tr><tr><td>168.119.10.134:26655</td><td>entangle_33133-1</td><td>TrustedPoint-1 🟢</td><td>2579484</td><td>2268001</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T16:04:55.799541721UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2579480</td><td>2272001</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T16:04:25.247653667UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>2579482</td><td>2304001</td><td>False</td><td>off</td><td>26809450365031740</td><td>2024-03-10T16:04:44.081824149UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>2579484</td><td>2436001</td><td>False</td><td>on</td><td>43265640813295039</td><td>2024-03-10T16:04:55.280942370UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2579483</td><td>2479483</td><td>False</td><td>off</td><td>46610916962884832</td><td>2024-03-10T16:04:50.654111261UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>2579482</td><td>2558001</td><td>False</td><td>on</td><td>505390570552930</td><td>2024-03-10T16:04:41.825402585UTC</td></tr></table>
