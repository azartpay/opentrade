# Azart Trade
### Open source cryptocurrency exchange for Azart 

Life version https://trade.azartpay.com/

Step-by-step install instructions:

1. Register on the VPS hosting like this https://www.digitalocean.com
2. Create "Droplet" Ubuntu 16 x64 / 1GB / 1vCPU / 25 GB SSD
3. Log in to Droplet console over SSH
4

```
sudo apt-get update
sudo apt-get install build-essential libssl-dev curl -y
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh -o install_nvm.sh
bash install_nvm.sh
sudo reboot

nvm install 6.0.0

git clone https://github.com/azartpay/azart-trade.git
cd azart-trade

sudo npm install 

mkdir ~/azart-trade/server/database
```

## Here is an example of file ~/azart-trade/server/modules/private_constants.js Edit as per your config.

```
'use strict';

exports.recaptcha_priv_key = 'YOUR_GOOGLE_RECAPTCHA_PRIVATE_KEY';
exports.password_private_suffix = 'LONG_RANDOM_STRING1';
exports.SSL_KEY = '../ssl_certificates/privkey.pem'; //change to your ssl certificates private key
exports.SSL_CERT = '../ssl_certificates/fullchain.pem'; //change to your ssl certificates fullchain

exports.walletspassphrase = {
    'AZART' : 'LONG_RANDOM_STRING2',
    'BTC' : 'LONG_RANDOM_STRING3',
    'DOGE' : 'LONG_RANDOM_STRING4'
};
```

**After all you can run exchange**

```
cd  ~/azart-trade/server
sudo node main.js
```

In the browser address string type https://127.0.0.1:40443
You will see Azart Trade.

The first registered user will be exchange administrator. 

# Add trade pairs

For each coin you should create *.conf file
This is common example for "some_coin.conf"

```
rpcuser=long_random_string_one
rpcpassword=long_random_string_two
rpcport=12345
rpcclienttimeout=10
rpcallowip=127.0.0.1
server=1
daemon=1
upnp=0
rpcworkqueue=1000
enableaccounts=1
litemode=1
staking=0
addnode=1.2.3.4
addnode=5.6.7.8

```

Also you must encrypt wallet.dat by the command

```
./bitcoind encryptwallet random_long_string_SAME_AS_IN_FILE_private_constants.js

```

*If coin is not supported encryption (like ZerroCash and it forks) then coin could not be added to the Azart Trade*


When coin daemons will be configured and started

1. Register on exchange. The first registered user will be exchange administrator.
2. Go to "Admin Area" -> "Coins" -> "Add coin"
3. Fill up all fields and click "Confirm"
4. Fill "Minimal confirmations count" and "Minimal balance" and uncheck and check "Coin visible" button
5. Click "Save"
6. Check RPC command for the coin. If it worked then coin was added to the exchange!

All visible coins should be appear in the Wallet. You shoud create default coin pairs now.

File ~/azart-trade/server/constants.js have constant that you can change

https://github.com/azartpay/azart-trade/blob/master/server/constants.js#L5

```
exports.TRADE_MAIN_COIN = "Azart"; //change Marycoin to your main coin pair
exports.TRADE_DEFAULT_PAIR = "Bitcoin"; //change Litecoin to your default coin pair
exports.TRADE_COMISSION = 0.001; //change trade comission percent

exports.recaptcha_pub_key = "6LeZ0WEUAAAAAG8hT0YzNPGga5W2ZpXNhr_acpG5"; //change to your recaptcha public key

exports.NOREPLY_EMAIL = 'no-reply@azartpay.com'; //change no-reply email
exports.SUPPORT_EMAIL = 'support@azartpay.com'; //change to your valid email for support requests
exports.my_portSSL = 40443; //change to your ssl port

```

After that you coins should appear on the main page.


