
# Lats Core Masternode Setup Guide

A short guide on how to create a Masternode for Lats Coin.

## Local Wallet Setup

These first steps are for the wallet that will be holding your Lats Collateral. (1000 LATS)

![Screenshot 2022-11-29 at 5 58 45 PM](https://user-images.githubusercontent.com/45834289/204674706-be64289f-ce64-4b48-bfd5-b7c87c1ca6bb.png)

If you have atleast 1,000 LATS coins, we can go to the MASTERNODES tab and from there select "Create Masternode Controller"

![Screenshot 2022-11-29 at 5 59 34 PM](https://user-images.githubusercontent.com/45834289/204674816-e02bcf3e-5db8-4225-a5f7-07852429fc04.png)

The masternode controller will walk you through the steps to setup everything required on your local wallet.

![Screenshot 2022-11-29 at 6 00 26 PM](https://user-images.githubusercontent.com/45834289/204674952-031e46fe-51ac-4e4b-9316-41e8c1291c31.png)

![Screenshot 2022-11-29 at 6 00 37 PM](https://user-images.githubusercontent.com/45834289/204674976-4212541c-fa62-48a3-a1df-e05367915955.png)

This screen we will have to add our name for the masternode, which if you see my screenshots mine are "Masternode1" but you can call it anything you like, many will commonly do "mn1" "mn2" so on and so forth.

![Screenshot 2022-11-29 at 6 01 39 PM](https://user-images.githubusercontent.com/45834289/204675068-e83bafde-5525-4465-973a-3d3d771f68f3.png)

This next screen is requesting the IP address for the VPS you have purchased in order to setup your masternode. A place that you can get one is from say, https://hostmaria.com. After clicking next, it will automatically send the coins to a new address and lock them to setup a masternode. The sent transaction requires atleast 15 confirmations before you can try starting the masternode, but that should be more than enough time to start configuring the VPS and it should all be ready by the time it is complete.

Upon completion we need to save some data we can get from our local wallet. If you are still in the masternode tab you need to click on the 3 dots next to your newly created masternode name. After clicking on it there is a tab called Info and it will have a copy button.


![Screenshot 2022-11-29 at 6 05 16 PM](https://user-images.githubusercontent.com/45834289/204675446-8a13d741-a733-4394-9627-a29e203d8830.png)

Now, we need to click on the copy button by "Export data to run the masternode on a remote server", this will copy to your clipboard information like the following:

```masternode=1
externalip=51.161.166.129
masternodeaddr=51.161.166.129:45454
masternodeprivkey=88wsw6D2KTQzSxEWD6WFYGtb9CcYqecGKA6UjTqkda313kr4VzD
```

We will save this information in a notepad somewhere for later after we start configuring our VPS.

## VPS Setup

This portion of the guide makes several assumptions:
- Already purchased a VPS
- Understanding of SSH
- Understanding of basic linux commands

For your VPS it is recommended to use minimally Ubuntu 18.04 for the Operating System.

Upon logging into your VPS with SSH, you will need to do several things

- Download the linux wallet
- Setup the lats.conf file
- Start the masternode
- Check the status

First things first lets update the system with the following commands
```
sudo apt-get update
sudo apt-get upgrade
```
This will take a few moments and upon completion we can simply run this command to download the wallet and extract it.

Now, you need to install unzip:
```
apt install unzip
```

Download the $Lats Core wallet for the Ubuntu 18.04:
```
wget https://github.com/LATS-DAO/Lats-Core/releases/download/v5.5.1/lats-core-ubuntu18.04-5.5.1.zip
```

and unzip it:
```
unzip lats-core-ubuntu18.04-5.5.1.zip
```
next, change the permissions:
```
chmod +x lat*
```

next, move all these new files to '/usr/local/bin/' that they can be valled from any location:
```
mv lat* /usr/local/bin/
```

Due to our coinhave the pre-requisites for Privacy Features like PIVX/ZCASH we need to make a directory for the sapling params so the wallet is able to run. Windows installer will do this automatically and same for the Mac .dmg.
Using these commands to set that up:
```
mkdir /root/.lats-params
cp /root/lats-5.5.1/share/lats/* /root/.lats-params
```
Next, we will configure our masternode we will start by making the default coin directory and configuration files below.
```
mkdir /root/.lats
nano /root/.lats/lats.conf
```
Here we will need to use that saved information from our local wallet and copy and paste it into the conf file.
You will also have to add the following
```
externalip=IP_HERE
rpcbind=127.0.0.1
bind=IP_HERE
rpcuser=supersecureusername
rpcpassword=supersecurepassword
rpcallowip=127.0.0.1
rpcport=45455
server=1
daemon=1
listen=1
port=45454
maxconnections=256
addnode=94.130.95.107
addnode=94.130.95.108
addnode=94.130.95.110
addnode=188.40.233.34
addnode=188.40.233.35
addnode=188.40.233.38
addnode=188.40.233.39
addnode=188.40.233.40
addnode=188.40.233.41
addnode=188.40.233.43
addnode=188.40.233.44
addnode=188.40.233.45
```
Theres a few modifications to the places, with IP_HERE we would replace with the IP address of the VPS that we are logged into. The RPC username/passwords need to be set for checking and talking to your masternode. RPC Port can be adjusted by Port can not.

Afterwards save and close the conf file.

Finally, we can start our masternode daemon on the server to sync!
```
./lats-5.5.1/bin/latsd 
```
This should initiate the daemon based on if you have been following the guide up until this point.

After waiting a few moments we can check the sync process by using
```
./lats-5.5.1/bin/lats-cli getblockcount
```
Once it matches the explorer https://explorer.lats.cc/ you can then go back to your local wallet on your normal PC and start the masternode.

Happy Masternoding!

Note: Please open a thread at the Masternodes section of the $Lats forum: https://forums.lats.cc/t/masternodes if you have any questions about this process, thoughts or suggestions.
