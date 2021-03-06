# The Bitcoin Block Clock

Raspberry Pi Full Node with 32 x 32 RGB LED network visualizer
-
### Video: https://www.youtube.com/watch?v=78u8EQtIXMY
### imgur gallery: https://imgur.com/a/KYPKK
-

### Dependencies:

* python-bitcoinrpc: https://github.com/jgarzik/python-bitcoinrpc (modified, included in this git as bitcoinrpc.py)

* Adafruit RGB LED matrix driver: https://github.com/adafruit/rpi-rgb-led-matrix/ 
Modified (see my fork: https://github.com/pinheadmz/rpi-rgb-led-matrix) already compiled and included in this git as rgbmatrix.so

* PyQRCode: https://pypi.python.org/pypi/PyQRCode:
```
$ sudo pip install pyqrcode
```

* Bitcoin Core (or alt-client, check out http://raspnode.com/diy.html) with the following lines added to `~/.bitcoin/bitcoin.config` (see Installation below, the paths should match):
```
blocknotify=python /home/pi/bin/ClockBlocker/block.py %s
walletnotify=python /home/pi/bin/ClockBlocker/tx.py %s
```

other helpful `bitcoin.config` parameters for running a full node on an RPi:
```
minrelaytxfee=0.00005000
limitfreerelay=0
dbcache=50
```
other tips for running a full node on an RPi:
* use an SSD drive (not a USB memory stick) for the blockchain
* Bitcoin Core version 0.12 employs `libsecp256k1` which improves block validation time a great deal


### Installation:

Clone this repository in ~/bin and make easy-to-type command to start clock:
```
$ cd ~/bin
$ git clone https://github.com/pinheadmz/ClockBlocker.git
$ ln -s ~/bin/ClockBlocker/ledbits.py ~/bin/ledbits
$ sudo chmod 577 ~/bin/ledbits
```
...then from any command line you can start the clock by entering:
````
$ ledbits
```



### API passwords:

* Bitcoin: create file `bitcoinAuth.py` which contains:
```
USER = "YOUR-BITCOIN-RPC-USERNAME"
PW = "YOUR-BITCOIN-RPC-PASSWORD"
```
* IP geo-location service: Sign up for API key at http://www.ipinfodb.com/ip_location_api.php

...then create file `ipInfoAuth.py` which contains:
```
api_username = 'YOUR-USERNAME'
api_pw = 'YOUR-PASSWORD'
api_key = 'YOUR-API-KEY'
```

### Hardware:
Here's a "wishlist" I made on Adafruit (accepts Bitcoin!) with most the components I used for the build:

https://www.adafruit.com/wishlists/394607

A few of these items might be found cheaper on other sites, but this is overall the shopping list.
I didn't include HDMI or USB cables, or the materials I used in my own "custom" power distributor, but that Adafruit 10A power supply is enough to run the entire system.

Here's the SSD I'm using for the blockchain:

http://www.amazon.com/gp/product/B00EZ2FRU2
