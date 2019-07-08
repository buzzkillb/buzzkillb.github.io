---
published: true
---
## Ledger Live

Playing around on Ubuntu 19.04, Disco Dingo to see how this all works. Trezor worked fine, but Ledger Live did not want to load, and then did not want to connect. So the 2 things I did to get Ledger Nano S working.  

This to be able to run Ledger Live  
```
sudo apt-get install --reinstall libgtk2.0-0
```
This to allow Ledger Live to connect to the Nano S.
```
wget -q -O - https://raw.githubusercontent.com/LedgerHQ/udev-rules/master/add_udev_rules.sh | sudo bash
```
link to official help on if you get more stuck than I did  
[https://support.ledger.com/hc/en-us/articles/115005165269-Fix-connection-issues](https://support.ledger.com/hc/en-us/articles/115005165269-Fix-connection-issues)
