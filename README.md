# UltraPayCoin
Shell script to install a [UltraPayCoin Masternode](https://ultrapay.info/) on a Linux server running Ubuntu 16.04 . Use it on your own risk.

## Installation of Libraries on VPS (using root user):
```
sudo su
add-apt-repository ppa:bitcoin/bitcoin -y
apt-get update 
apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils 
apt-get install -y libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev 
apt-get install -y libdb4.8-dev libdb4.8++-dev 
apt-get install libminiupnpc-dev 
apt-get install libzmq3-dev
apt-get update
```


***
## Installation (latest wallet version):
```
git clone https://github.com/upc-dev-team/UPCinstall.git
cd UPCinstall
bash upc-install.sh
```
***
## Update wallet to latest version:
```
cd ~/UPCinstall/
git pull
bash upc-update.sh
```
***

## Desktop wallet setup

After the MN is up and running, you need to configure the desktop wallet accordingly. Here are the steps for Windows Wallet
1. Open the UltraPayCoin Coin Desktop Wallet.
2. Go to RECEIVE and create a New Address: **MN1**
3. Send **6000** **UPC** to **MN1**.
4. Wait for 15 confirmations.
5. Go to **Tools -> "Debug console - Console"**
6. Type the following command: **masternode outputs**
7. Go to  ** Tools -> "Open Masternode Configuration File"
8. Add the following entry:
```
Alias Address Privkey TxHash Output_index
```
* Alias: **MN1**
* Address: **VPS_IP:PORT**
* Privkey: **Masternode Private Key**
* TxHash: **First value from Step 6**
* Output index:  **Second value from Step 6**
9. Save and close the file.
10. Go to **Masternode Tab**. If you tab is not shown, please enable it from: **Settings - Options - Wallet - Show Masternodes Tab**
11. Click **Update status** to see your node. If it is not shown, close the wallet and start it again. Make sure the wallet is unlocked.
12. Open **Debug Console** and type:
```
startmasternode "alias" "0" "MN1"
```
***

## Usage (on VPS):
```
ultrapaycoin-cli getinfo
ultrapaycoin-cli mnsync status
ultrapaycoin-cli masternode status
```
Also, if you want to check/start/stop **UltraPayCoin** , run one of the following commands as **root**:

**Ubuntu 16.04**:
```
systemctl status UltraPayCoin #To check the service is running.
systemctl start UltraPayCoin #To start UltraPayCoin service.
systemctl stop UltraPayCoin #To stop UltraPayCoin service.
systemctl is-enabled UltraPayCoin #To check whetether UltraPayCoin service is enabled on boot or not.
```
**Ubuntu 14.04**:  
```
/etc/init.d/UltraPayCoin start #To start UltraPayCoin service
/etc/init.d/UltraPayCoin stop #To stop UltraPayCoin service
/etc/init.d/UltraPayCoin restart #To restart UltraPayCoin service
```
***
