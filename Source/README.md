[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Source)
=

# SnapShot (~0.1 GB) updated every 10 hours
```python
cd $HOME
sudo systemctl stop sourced
cp $HOME/.source/data/priv_validator_state.json $HOME/.source/priv_validator_state.json.backup
rm -rf $HOME/.source/data
wget http://source.snapshot.stavr.tech:5003/source/source-snap.tar.lz4 && lz4 -c -d $HOME/source-snap.tar.lz4 | tar -x -C $HOME/.source --strip-components 2
rm -rf source-snap.tar.lz4
wget http://source.wasm.stavr.tech:1000/wasm-snap.tar.lz4 && lz4 -c -d $HOME/wasm-snap.tar.lz4 | tar -x -C $HOME/.source/data --strip-components 3
rm -rf wasm-snap.tar.lz4
mv $HOME/.source/priv_validator_state.json.backup $HOME/.source/data/priv_validator_state.json
sudo systemctl restart sourced && journalctl -u sourced -f -o cat
```
