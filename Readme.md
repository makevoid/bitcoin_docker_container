# Counterparty blockchian machine setup

```sh
echo "deb http://http.debian.net/debian oldstable main" >> /etc/apt/sources.list

# packages
apt-get update
apt-get install libdb4.8-dev libdb4.8++-dev  -y
sed -i '$ d' /etc/apt/sources.list # removes the last line

apt-get update
apt-get install build-essential vim wget libtool autotools-dev pkg-config autoconf libssl-dev libboost-all-dev bsdmainutils   -y

# get patched bitcoin
mkdir ~/tmp
cd ~/tmp
wget https://github.com/btcdrak/bitcoin/releases/download/addrindex-0.10.0/bitcoin-addrindex-0.10.0.tar.gz
tar xvf bitcoin-addrindex-0.10.0.tar.gz

# configure
cd bitcoin-0.10.0
./configure
make
make install


echo "
rpcuser=bitcoin
rpcpassword=EDITME
server=1
daemon=1
rpcthreads=1000
rpctimeout=300
txindex=1
addrindex=1
" > /root/.bitcoin/bitcoin.conf

# starts bitcoind
bitcoind

# manually: check if there are connections
bitcoin-cli getinfo

# TODO: setup bitcoind in init.d

# docker commit <container_id> counterparty_no_chain
# more infos: http://counterparty.io/docs/bitcoin_core/
# docker push makevoid/counterparty_no_chain
```
