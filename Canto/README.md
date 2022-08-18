# SnapShot 18.08.22 (0.1 GB) block height --> 331429
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop cantod
rm -rf $HOME/.cantod/data/
mkdir $HOME/.cantod/data/

# download archive
cd $HOME
wget http://116.202.236.115:7000/cantodata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf cantodata.tar.gz --strip-components 1
№ Download priv_validator_state.json 
wget -O $HOME/.cantod/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Canto/priv_validator_state.json"
# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm cantodata.tar.gz
# start the node
sudo systemctl restart cantod && journalctl -u cantod -f -o cat
```
