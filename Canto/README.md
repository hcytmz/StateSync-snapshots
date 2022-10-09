[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Canto)
=
# SnapShot 09.10.22 (0.1 GB) block height --> 1109858
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop cantod
rm -rf $HOME/.cantod/data/
mkdir $HOME/.cantod/data/

# download archive
cd $HOME
wget http://canto.snapshot.stavr.tech:6001/cantodata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf cantodata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.cantod/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Canto/priv_validator_state.json"
cd && cat .cantod/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}
# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm cantodata.tar.gz
# start the node
sudo systemctl restart cantod && journalctl -u cantod -f -o cat
```
