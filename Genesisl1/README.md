# Snaphot (57 GB) height 4598847
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
systemctl stop genesisd
rm -rf $HOME/.genesisd/data/
mkdir $HOME/.genesisd/data/

# download archive
cd $HOME
wget http://65.108.6.45:8000/genesisl1/l1data.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf l1data.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm genesisddata.tar.gz
systemctl restart genesisd && journalctl -u genesisd -f -o cat
```
