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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>1990762</td><td>1</td><td>False</td><td>off</td><td>280971187098421</td><td>2024-02-03T02:17:27.278475806UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1990762</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T02:17:28.347948639UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1990765</td><td>1</td><td>False</td><td>off</td><td>27051591708235960</td><td>2024-02-03T02:17:42.236578544UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1990767</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T02:17:49.202097738UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>1990767</td><td>1</td><td>False</td><td>on</td><td>163468493211859</td><td>2024-02-03T02:17:51.899791604UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>1990765</td><td>660001</td><td>False</td><td>on</td><td>123694976944316</td><td>2024-02-03T02:17:44.532364620UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1990762</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-02-03T02:17:26.946073257UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1990763</td><td>962001</td><td>False</td><td>on</td><td>324096560670359</td><td>2024-02-03T02:17:30.800527910UTC</td></tr><tr><td>89.117.63.35:14257</td><td>entangle_33133-1</td><td>VTB-ENTANGLE 🟢</td><td>1990764</td><td>1162001</td><td>False</td><td>off</td><td>0</td><td>2024-02-03T02:17:39.645193908UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1990762</td><td>1312001</td><td>False</td><td>off</td><td>461402470413526</td><td>2024-02-03T02:17:27.647515093UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1990767</td><td>1716001</td><td>False</td><td>on</td><td>43682191727197074</td><td>2024-02-03T02:17:51.598797981UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1990766</td><td>1890766</td><td>False</td><td>off</td><td>46577060135439788</td><td>2024-02-03T02:17:46.838404989UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>1990763</td><td>1910001</td><td>False</td><td>off</td><td>303802704279276</td><td>2024-02-03T02:17:31.074480463UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>1990765</td><td>1958001</td><td>False</td><td>on</td><td>477140539434549</td><td>2024-02-03T02:17:41.989498455UTC</td></tr><tr><td>86.48.0.190:15657</td><td>entangle_33133-1</td><td>vmi1185834.contaboserver.net 🟢</td><td>1980714</td><td>1961001</td><td>False</td><td>off</td><td>0</td><td>2024-02-03T02:17:27.990764174UTC</td></tr><tr><td>212.22.70.9:56657</td><td>entangle_33133-1</td><td>Sr20de 🟢</td><td>1990762</td><td>1971001</td><td>False</td><td>off</td><td>0</td><td>2024-02-03T02:17:26.590228254UTC</td></tr></table>
