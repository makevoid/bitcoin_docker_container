# Bitcoin machine setup

go to bitcoin.org

wget the linux-64 version

enter the bin dir

run 

    ./bitcoind


create and edit bitcoin.conf

    vim ~/bitcoin/bitcoin.conf


enter a screen session (optional but useful, your shell/terminal session will be persisted even if the ssh connection closes)

    screen
    
then press enter



launch bitcoind

    ./bitcoind -prune=4000


the command should output nothing, open another ssh session then type


    tail -f ~/.bitcoin/debug.log

it should output some commands



then do a docker commit when you downloaded the chain 

put the docker/vm hash and the md5 hash of the image file maybe in the blockchain using some services like <eternitywall.it>, <cryptograffiti.info> etc...

reuse everytime!

save, commit, hash, share, repeat...

enjoy your bitcoin+blockchain secure distributed installation


----

Further use:

enter bitcoin-cli

    bitcoin-cli balance
    
    
    bitcoin-cli accounts

    bitcoin-cli getaccountaddress ""
    
    bitcoin-cli dumpprivkey
    
    bitcoin-cli sendtoaddress "1address...", 0.0001
    
    


---
More and more use:

Use an HTTP library and some JSON to communicate to bitcoind server using the JSON RPC or websocket / zmq API.

Much power.

---

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

# for bitcoin (recommended)
wget 

# or for bitcoin w/ counterparty patch (old v)
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
