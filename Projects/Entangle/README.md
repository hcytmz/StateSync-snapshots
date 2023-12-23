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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>1267320</td><td>1</td><td>False</td><td>off</td><td>259586473635098</td><td>2023-12-22T23:39:39.334891560UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1267323</td><td>1</td><td>False</td><td>off</td><td>47049700500000000</td><td>2023-12-22T23:39:51.846563875UTC</td></tr><tr><td>54.159.151.199:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1267324</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-22T23:39:59.202941926UTC</td></tr><tr><td>54.196.43.239:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1267324</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-22T23:39:59.835683364UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>1267325</td><td>1</td><td>False</td><td>on</td><td>59519660338000</td><td>2023-12-22T23:40:00.873381088UTC</td></tr><tr><td>144.76.174.27:17357</td><td>entangle_33133-1</td><td>kokos 🔴</td><td>1267322</td><td>145001</td><td>False</td><td>on</td><td>89890100000000</td><td>2023-12-22T23:39:48.774935655UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>1267324</td><td>660001</td><td>False</td><td>on</td><td>37511111100000</td><td>2023-12-22T23:39:54.169059976UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1267320</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2023-12-22T23:39:39.079018057UTC</td></tr><tr><td>158.220.91.214:17157</td><td>entangle_33133-1</td><td>Iryna2 🔴</td><td>1267325</td><td>704001</td><td>False</td><td>on</td><td>180890937000019</td><td>2023-12-22T23:40:00.288443945UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>1267321</td><td>725001</td><td>False</td><td>on</td><td>180899900000002</td><td>2023-12-22T23:39:44.378101460UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1267320</td><td>806001</td><td>False</td><td>off</td><td>261143217535902</td><td>2023-12-22T23:39:39.683157405UTC</td></tr><tr><td>95.216.10.232:28857</td><td>entangle_33133-1</td><td>SRG0Z10 🔴</td><td>1267320</td><td>842001</td><td>False</td><td>off</td><td>17477251056590</td><td>2023-12-22T23:39:36.702135248UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1267321</td><td>962001</td><td>False</td><td>on</td><td>314013548351851</td><td>2023-12-22T23:39:44.062337879UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>1267322</td><td>1054001</td><td>False</td><td>on</td><td>201531178365442</td><td>2023-12-22T23:39:51.543190697UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1267325</td><td>1076001</td><td>False</td><td>on</td><td>44568809900999996</td><td>2023-12-22T23:40:00.544507765UTC</td></tr><tr><td>89.117.63.35:14257</td><td>entangle_33133-1</td><td>VTB-ENTANGLE 🔴</td><td>1267322</td><td>1162001</td><td>False</td><td>off</td><td>95826514071325</td><td>2023-12-22T23:39:49.177829291UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1267324</td><td>1167324</td><td>False</td><td>off</td><td>46574292273662988</td><td>2023-12-22T23:39:58.498440460UTC</td></tr></table>
