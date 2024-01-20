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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>1776335</td><td>1</td><td>False</td><td>off</td><td>259586473635098</td><td>2024-01-20T08:08:16.980223481UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1776337</td><td>1</td><td>False</td><td>off</td><td>47049700500000000</td><td>2024-01-20T08:08:27.411344046UTC</td></tr><tr><td>34.116.174.56:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1776337</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T08:08:32.194540780UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1776338</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T08:08:32.887436282UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🟢</td><td>1776338</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T08:08:33.791307686UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1776337</td><td>660001</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T08:08:29.680728297UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1776335</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-01-20T08:08:16.646902212UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>1776336</td><td>725001</td><td>False</td><td>on</td><td>215523891990001</td><td>2024-01-20T08:08:21.985826580UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1776336</td><td>962001</td><td>False</td><td>on</td><td>310873412868333</td><td>2024-01-20T08:08:21.709521215UTC</td></tr><tr><td>89.117.63.35:14257</td><td>entangle_33133-1</td><td>VTB-ENTANGLE 🟢</td><td>1776336</td><td>1162001</td><td>False</td><td>off</td><td>0</td><td>2024-01-20T08:08:26.654191160UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1776335</td><td>1312001</td><td>False</td><td>off</td><td>361496835362747</td><td>2024-01-20T08:08:17.378101516UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>1776337</td><td>1436001</td><td>False</td><td>on</td><td>454417023854259</td><td>2024-01-20T08:08:27.065779140UTC</td></tr><tr><td>158.220.91.214:17157</td><td>entangle_33133-1</td><td>Iryna2 🔴</td><td>1776338</td><td>1440001</td><td>False</td><td>on</td><td>278277208343724</td><td>2024-01-20T08:08:33.204968417UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1776337</td><td>1676337</td><td>False</td><td>off</td><td>46574292273662988</td><td>2024-01-20T08:08:32.472170829UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1776338</td><td>1716001</td><td>False</td><td>on</td><td>44123121801989996</td><td>2024-01-20T08:08:33.462605966UTC</td></tr></table>
