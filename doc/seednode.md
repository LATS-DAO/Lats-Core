# Creating a Seednode for Lats Core

## Preface

A seed node is one of the main IP's wallets/masternodes/peers connect to in order to get blockchain data. In attempts to become more decentralized this should be some community members to help promote more network connectivity and decentralization.

This guide assumes basic Linux knowledge/SSH knowledge as the guide is going through the setup on a Linux based VPS that is already purchased. You can actually setup a seed node on any computer running 24/7 and the main focus is the lats.conf file being modified appropriately.

## Seednode Setup

Login to your Linux VPS through SSH

First steps would be downloading and unzipping the wallet files.

```
wget https://github.com/LATS-DAO/Lats-Core/releases/download/3.0.0/lats-3.0.0-x86_64-linux-gnu.tar.gz && tar -xvf lats-3.0.0-x86_64-linux-gnu.tar.gz
```

After unzipping we will make our .lats-params directory and setup the .lats directory and lats.conf

```
mkdir /root/.lats-params
mkdir /root/.lats
nano /root/.lats/lats.conf
```

The last line opens the text editor to modify the conf file, to which just copy and paste the following

```
daemon=1
server=1
listen=1
maxconnections=512
rpcuser=somesupersecureuser
rpcpassword=somesupersecurepassword
rpcport=45444
port=45454
bind=IPHERE
addnode=188.40.233.40
addnode=188.40.233.41
addnode=188.40.233.39
```

That is all! Now just run the daemon with the following command.

```
/root/lats-3.0.0/bin/latsd
```

The key portions of a seed node is allowing a lot of connections to the node and the best uptime possible to provide connectivity for users and services.
