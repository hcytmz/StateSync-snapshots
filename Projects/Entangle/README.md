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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2524850</td><td>1</td><td>False</td><td>off</td><td>309230764490552</td><td>2024-03-07T07:28:16.965722437UTC</td></tr><tr><td>34.118.4.252:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2524851</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T07:28:19.788402943UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2524854</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T07:28:41.783868131UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2524854</td><td>1</td><td>False</td><td>on</td><td>213864609130961</td><td>2024-03-07T07:28:44.372725377UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2524853</td><td>660001</td><td>False</td><td>on</td><td>180069059856284</td><td>2024-03-07T07:28:35.042621663UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2524851</td><td>1312001</td><td>False</td><td>off</td><td>549935311814865</td><td>2024-03-07T07:28:17.311632388UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>2524851</td><td>1910001</td><td>False</td><td>off</td><td>330391081392576</td><td>2024-03-07T07:28:22.086497103UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2524850</td><td>2049001</td><td>False</td><td>off</td><td>29239683913065</td><td>2024-03-07T07:28:16.717652926UTC</td></tr><tr><td>168.119.10.134:26655</td><td>entangle_33133-1</td><td>TrustedPoint-1 🟢</td><td>2524854</td><td>2268001</td><td>False</td><td>off</td><td>0</td><td>2024-03-07T07:28:44.592459995UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2524850</td><td>2272001</td><td>False</td><td>on</td><td>0</td><td>2024-03-07T07:28:16.403091019UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>2524852</td><td>2304001</td><td>False</td><td>off</td><td>26809201862623766</td><td>2024-03-07T07:28:32.757247741UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>2524852</td><td>2327001</td><td>False</td><td>on</td><td>503661823681206</td><td>2024-03-07T07:28:32.552632935UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2524853</td><td>2424853</td><td>False</td><td>off</td><td>46610776233046312</td><td>2024-03-07T07:28:39.316164389UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>2524854</td><td>2436001</td><td>False</td><td>on</td><td>43265548787075332</td><td>2024-03-07T07:28:44.074466586UTC</td></tr></table>
