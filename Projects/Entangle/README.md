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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>847163</td><td>1</td><td>False</td><td>91742435553176</td><td>2023-11-29T20:07:29.732428215UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>847165</td><td>1</td><td>False</td><td>47049700500000000</td><td>2023-11-29T20:07:40.984505119UTC</td></tr><tr><td>54.159.151.199:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>847166</td><td>1</td><td>False</td><td>0</td><td>2023-11-29T20:07:48.283277204UTC</td></tr><tr><td>54.196.43.239:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>847166</td><td>1</td><td>False</td><td>0</td><td>2023-11-29T20:07:48.959955133UTC</td></tr><tr><td>35.175.80.14:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>847166</td><td>1</td><td>False</td><td>0</td><td>2023-11-29T20:07:52.207494509UTC</td></tr><tr><td>5.161.58.198:17157</td><td>entangle_33133-1</td><td>Gumat.top 🔴</td><td>847166</td><td>522001</td><td>False</td><td>40931860000000</td><td>2023-11-29T20:07:52.893867983UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>847166</td><td>531401</td><td>False</td><td>44568809900999996</td><td>2023-11-29T20:07:51.570586008UTC</td></tr><tr><td>212.22.70.9:56657</td><td>entangle_33133-1</td><td>Sr20de 🟢</td><td>847163</td><td>620601</td><td>False</td><td>0</td><td>2023-11-29T20:07:29.224224884UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>847165</td><td>660001</td><td>False</td><td>0</td><td>2023-11-29T20:07:43.310086475UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>847163</td><td>660801</td><td>False</td><td>0</td><td>2023-11-29T20:07:29.491761778UTC</td></tr><tr><td>158.220.91.214:17157</td><td>entangle_33133-1</td><td>Iryna2 🟢</td><td>847166</td><td>704001</td><td>False</td><td>0</td><td>2023-11-29T20:07:49.285834391UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>847166</td><td>747166</td><td>False</td><td>46564769273662988</td><td>2023-11-29T20:07:47.653524562UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>847163</td><td>806001</td><td>False</td><td>113571482790726</td><td>2023-11-29T20:07:30.156886763UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🟢</td><td>847165</td><td>822001</td><td>False</td><td>0</td><td>2023-11-29T20:07:40.752855573UTC</td></tr></table>
