# SnapShot 17.08.22 (0.1 GB) block height --> 324300
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

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm cantodata.tar.gz
# start the node
sudo systemctl restart cantod
```
