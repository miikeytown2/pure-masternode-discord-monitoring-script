# Table of Contents
1. [Quick Guide](#quick-guide)
1. [Masternode Guide](#masternode-guide)
1. [Quick and easy VPS guide](#quick-and-easy-vps-guide)
1. [Pure Masternode Discord Monitoring Script](#pure-masternode-discord-monitoring-script)
1. [Troubleshooting / FAQ](#troubleshooting--faq)
1. [Appendix](#appendix)
1. [Pure Tip Address](#pure-tip-address)

---
---

# Quick Guide
On your VPS run this to get Alias, Address, PrivKey and a pure masternode daemon ready to go.  
#### `bash -c "$(wget -qO- -o- goo.gl/FWMqpe)"`  
`O` is the letter not the number if you are typing this out.  
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) is highly recommended in order to use copy/paste.  
You can view the script here https://goo.gl/FWMqpe  
At the prompts press enter to use the defaults (recommended).

___  
___  

# Masternode Guide
What you need:  
- A Ubuntu 16.04 OR 18.04 Virtual Private Server ([VPS](https://www.vultr.com/?ref=7333199)) for running the masternode  
- A way to use SSH ([PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) for windows or Terminal for Mac)  
- Pure Wallet ([Win](https://github.com/puredev321/pure/releases/latest)) ([Mac](https://drive.google.com/open?id=1-o0dUcVpz6u9rpLtwWs1lxrC5Sklrn0N)) with [5000.1 Pure](https://www.coinexchange.io/market/PURE/BTC?r=f0466c8f)  
- Help can be found on the [Discord chat](https://discord.gg/wEBB4Ys)

<details><summary>Info needed from VPS masternode:</summary>
  
`bash -c "$(wget -qO- -o- goo.gl/FWMqpe)"`  
Run this on a VPS to generate the following values.  
Or if you already ran the script run this to get the values and you forgot to copy the values.  
`head -20 /home/mn1/.pure/pure.conf`  
</details>

- Alias  
- Address  
- PrivKey  

<details><summary>Info needed from Pure wallet:</summary>
  
Help -> Debug Window -> Console from the toolbar and type in `masternode outputs` at the bottom  

</details>

- TxHash  
- Output Index  
- Reward Address  
- Reward %  

Open up a text editor like notepad; this will be used to copy various bits of text to.

Transfer all your coins from the exchange to your wallet. In your pure wallet go Settings -> Unlock Wallet. Next on the left side select the Receive tab and create 2 new Addresses called *MN1_payout* and *MN1*. The *MN1_payout* address will be your Reward Address; copy the payout address to notepad and type in 100 on the next line. Copy the *MN1* address  and go to send tab. In "Pay To:" paste in the address and send **exactly 5000** in a single transaction; no more, no less; **5000**. At this stage notepad should look like this

    PXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    100


Once the transaction of 5000 has hit the blockchain (1 block/~1 minutes) select Help -> Debug Window -> Console from the toolbar and type in `masternode outputs` at the bottom. The long string is the *TxHash* and the short string (usually a 0 or 1) is the *Output Index* (remove any extra quotes from both of these); a colon `:` separates these. Copy these values to the top of notepad one per line. At this stage notepad should look like this; remember Output Index can be a 0 or 1.

    xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    1
    PXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    100

Once you have the VPS running (see [Quick and easy guide below](#quick-and-easy-vps-guide)) the script will output Alias, Address, PrivKey. Copy these to notepad above the TxHash. At this stage notepad should look like this

    mn1_vultr.guest
    1.2.3.4:56789
    XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    1
    PXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
    100

In the Wallet go Settings -> Unlock Wallet. Next on the left side select Masternodes -> My Master Nodes -> Create... and input the needed values; set Reward % to 100. Example values below

             Alias: mn1_vultr.guest
           Address: 1.2.3.4:56789
           PrivKey: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
            TxHash: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      Output Index: 0
    Reward Address: PXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
          Reward %: 100


<details><summary>Click here for an explanation of the values used to create a Pure masternode</summary>
  
The top 3 values come from the Virtual Private Server. The Alias is a value used to let you know what this masternode should be called in your wallet; this can be set to anything as long as there are no spaces in it. The Address is the IP and Port of the VPS. PrivKey is how the masternode running on the VPS knows instructions given to it are valid; it's like a password for the masternode software running on the VPS.  
The TxHash & Output Index come from the blockchain. It's the transaction ID from the transfer of 5000 pure to the MN1 address. Once you have moved the 5000 into the new address you can look for the PURE txid in the [Block Explorer](http://purexplorer.dynu.net/). In the search bar input the MN1 Address and then click the Hash. The PURE txid is listed, this is the TxHash. The Output Index can be found by looking at Recipients; first Address has an output index of 0, second has an output index of 1; the one with 5000 is the Output Index you want to use.  
Reward Address is where the coins that the masternode has collected go.  
Reward % is the split of the masternode wallet and the Reward Address. Always set this to 100.  

</details>

![](https://i.imgur.com/U3kmiFL.png)![](https://i.imgur.com/SO0JbT3.png)  


Once created click Update button below to have the masternode appear. Select the new masternode and press the start button. Press update button again and make sure the status says "Masternode is running". If you just transferred 5000 coins to the MN1 address you'll need to wait for it to be confirmed before you can start the Masternode; this is 15 blocks or 15 minutes.

Wait 30-60 minutes and check the Pure Network under Masternodes tab; you should see the IP and port in the list.

# Quick and easy VPS guide #
### Get a VPS from here ###
https://www.vultr.com/?ref=7333199

Once signed up go here https://my.vultr.com/deploy/ 
1. Select a location (not all offer $2.50 servers)
2. Select Ubuntu 16.04
3. Select $2.50
- Click deploy now button

Once deployed (wait 2 minutes) click the Manage button on the right

Under IP click the copy icon 
![copy icon](https://www.materialui.co/materialIcons/content/content_copy_black_24x24.png "copy icon" )  


### Windows ###
<details><summary>Click here to read Windows SSH instructions</summary>
 
Open up [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and on the left hand side select Session  
![PuTTY ssh auth](https://linode.com/docs/assets/putty-configuration-window.png "PuTTYgen ssh auth")  
Paste in the IP of your VPS into the Host Name (or IP address) field. Now is a good time to save the session.
Now click open. Click Yes on the PuTTY Security Alert popup.  
![Security Alert](https://www.ssh.com/s/putty-security-alert-431x298-mqLph86E.png "Security Alert")  
`login as: root`  
Go back to the vultr manage webpage and under password click the copy icon 
![copy icon](https://www.materialui.co/materialIcons/content/content_copy_black_24x24.png "copy icon")  
Back on the PuTTY screen right click (right click is paste) and press enter to fill in the password. 
`root@x.x.x.x's password:`  

 </details>
 
___  

### Mac ###
<details><summary>Click here to read Mac SSH instructions</summary>
 
Finder -> Menubar (top of screen) -> Go -> Utilities. Open Terminal. Type in  
`ssh root@` and then go to the menu bar and select edit -> paste (the IP address).  
`The authenticity of host 'x.x.x.x (x.x.x.x)' can't be established.  
ECDSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxx.  
Are you sure you want to continue connecting (yes/no)? yes` Type in yes here  
`root@x.x.x.x's password: `  
Go back to the vultr manage webpage and under password click the copy icon 
![copy icon](https://www.materialui.co/materialIcons/content/content_copy_black_24x24.png "copy icon")  
Back on the Terminal screen paste in the password and press enter.  

</details>

___

Run this and you'll have a master node ready to use in under an hour. Copy the following line and paste into your remote terminal and press enter.  
#### `bash -c "$(wget -qO- -o- goo.gl/FWMqpe)"`  
`O` is the letter not the number if you are typing this out.  
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) is highly recommended in order to use copy/paste.  
Press Enter at the prompts to use the defaults. If setting up more than one master node re-run the script and input a different username (like mn2).  

You can view the script here https://goo.gl/FWMqpe

Also be mindfull when sending 5000 coins to the *MN2* address; by default the coins from *MN1* will be transfered to *MN2*. To Avoid this situation you'll want to use coin control. Go to Settings -> Options -> Display: Check Display coin control features (expers only!); select the Send tab on the left and under Coin Control Features click Inputs...; check all boxes other than your Master node addresses that contain 5000 Pure and hit OK; put in your *MN2* address, set amount to 5000, unlock wallet, and click Send.  

Script will end with  
- Auto starting pured daemon running under the newly created user  
- Suggested Alias  
- Address  
- PrivKey  

Go back to the start of this guide to see what to do with Alias, Address, & PrivKey.

If you messed up and want to start over with a fresh VPS instance go to https://my.vultr.com/ click on the three dots to the right ... and select Server Reinstall.

---
---

# Pure Masternode Discord Monitoring Script

You'll need to create a new discord server by pressing the + button on the left, call it what ever you want like "PURE masternode log". Right click on your newly created server icon (upper left corner) -> Server Settings -> Webhooks' -> Create Webhook -> Copy webhook url -> save.

It'll let you know when you've mined a block, if your mn status is not 9, if pured is not running, if blockcount is behind, if connection count is low, and it'll ping every 2 hours to let you know that the monitor is running. It installs as a service so it should come up on system reboot.

#### `bash -c "$(wget -qO- -o- goo.gl/uh7YAy)"`
`O` is the letter not the number if you are typing this out.  
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) is highly recommended in order to use copy/paste.  
You can view the script here https://goo.gl/uh7YAy

---
---

# Troubleshooting / FAQ  
#### Masternodes/Staking Reward Amount  
Masternodes get 100 Pure as a reward, Staking gets 20 Pure as a reward; total block reward is 120. You can't have the same 5000 coins used for running the masternode also Staking; your wallet will enforce this limitation automatically.

#### Masternodes Reward Time  
Masternodes rewards are by chance ([read more about the odds here](https://magnetwork.io/2018/02/26/masternode-rewards-in-question/)). Most will be in the middle of the bell curve but sometimes you'll be very lucky or very unlucky.   
![](https://i.imgur.com/MeeY1D1.gif)   
With [1440 Active Masternodes](https://masternodes.online/currencies/PURE/) running you can expect 7 rewards a week at the center of the bell curve. When more masternodes are running, the payout time increases, netting you less coins.

 

#### Staking Reward Time  
Staking rewards are by chance. You have to have your computer with the wallet running 24/7 for this to work; you can [calculate the cost here](https://www.rapidtables.com/calc/electric/energy-cost-calculator.html) of having it on 24/7. To see if Staking is working hover over the green icon in the lower right corner of the wallet. Staking does not work if your computer is in Sleep mode.

#### Can I run a masternode on my home computer?
Technically yes. You need a static IP from your ISP as well as a way to open up the port that your masternode is running on in your router. A VPS is easier to setup and run.

#### Could not allocate vin  
Unlock the wallet and try again. Make sure 15 blocks have passed (15 minutes) since the transfer to your MN1 address has passed. If the error still happens try closing your wallet, wait for the masternode list to sync and then try starting up your masternode again once you have unlocked your wallet. If you have mutiple pure gui wallets open on mutiple computers this can also happen; only have 1 wallet open before trying to start the masternode.

If you moved coins around this error can also happen. Quickest way to verify that the masternode still has valid coins is to go to Help -> Debug Window -> Console and type in `masternode outputs`. If the TxHash of your masternode is not listed then the masternode address no longer contains exactly 5000 Pure. To see the amount of Pure in each Addresses Go to Settings -> Options -> Display: Check `Display coin control features (expers only!)`; select the Send tab on the left and under Coin Control Features click `Inputs...`; The Coin Control dialog box should show the various Labels and how much Pure address contains. You'll need to move coins around to make sure that all your masternode addresses contain 5000 Pure via a single transaction per address (Send 5000). Once done run `masternode outputs` and reinput the data in the Masternodes -> My Master Nodes -> Create dialog box; you don't need to change anything on your VPS.

#### Just started the masternode and 30 minutes later I see "Not in the Masternode list" for my masternode  
Sometimes when starting a brand new masternode it can say it started when in reality it didn't. Simply start it again and wait 30 minutes to check and see that it's been started.

#### Started Wallet and I see "Not in the Masternode list" for my masternode  
You need to wait for all Masternodes to appear in the list; otherwise the state of your masternode from the wallet will not be accurate. Wait for the Pure Node Count to be equal to the [number of active Masternodes listed here](https://masternodes.online/currencies/PURE/) and then press the update button. The masternode list building process is slow.

#### How do I backup my wallet?  
Make sure it's been encrypted with a password and then store the wallet.dat file on [Dropbox](https://www.dropbox.com/) or [Google Drive](https://drive.google.com/). Make sure the cloud backup provider has 2 factor authentication enabled ([Google](https://support.google.com/accounts/answer/185839?hl=en), [Dropbox](https://www.dropbox.com/help/security/enable-two-step-verification)). On windows the wallet can be found in the `%appdata%/Pure` directory (windows key + r `%appdata%/Pure` and if that doesn't work try `%userprofile%\AppData\Roaming\Pure`). On Mac it can be found in the `~/Library/Application Support/Pure` directory; Finder -> Menubar (top of screen) -> Go -> Utilities, open Terminal, type in `open ~/Library/Application\ Support/Pure`.

#### My VPS got restarted and now my masternode is not running.
You need to start the Masternode again. Unlock the Wallet. Pure - Wallet -> Masternodes -> My Master Nodes, Select the masternode click update, click start, click update. It should be running again.

#### 0 active connections with pure network
You might need to add peers on your wallet manually due to your routers firewall configuration. Copy the [Addnodes text on the left](https://www.coinexchange.io/network/peers/PURE) into your pure.conf or qt.conf at the bottom of the file. This file is located in the `%appdata%/Pure` directory on Windows (windows key + r `%appdata%/Pure` and if that doesn't work try `%userprofile%\AppData\Roaming\Pure`) and `~/Library/Application Support/Pure` directory on Mac. Paste all `addnode=1.2.3.4` lines into the file; this can be copied by pressing the copy addnodes button at the bottom of the list.

#### Blockcount in wallet is behind
Help -> Debug Window -> Console and type in `checkwallet`. If it doesn't say `"wallet check passed" : true` then run `repairwallet` and run `checkwallet` again. If all checks pass restart the Pure Wallet.  

If the blockcount is still not updating follow the directions for [0 active connections with pure network](#0-active-connections-with-pure-network) in this guide.

If the blockcount is still not updating then follow the directions for being [stuck on the 1.0.0.2 blockchain](#stuck-on-the-1002-blockchain).

#### Stuck on the 1.0.0.2 blockchain  
1. Upgrade to 1.0.0.3 if you haven't already done so.
2. Close Pure all the way; shut it down.
3. Backup these file if they exist: `wallet.dat`, `masternode.conf`, `pure.conf`, and `qt.conf` from the Pure directory; Windows: `%appdata%/Pure` (windows key + r `%appdata%/Pure` and if that doesn't work try `%userprofile%\AppData\Roaming\Pure`), Mac: `~/Library/Application Support/Pure` (on mac to get to this directory go to Finder -> Menubar (top of screen) -> Go -> Utilities, open Terminal, type in `open ~/Library/Application\ Support/Pure`).
4. Delete everything in the Pure directory EXCEPT for `wallet.dat`, `masternode.conf`, `pure.conf`, `qt.conf`, and the `backups` filder (There should be 2-3 files left depending on if you have a masternode setup).
5. Copy the [Addnodes text on the left](https://www.coinexchange.io/network/peers/PURE) into your pure.conf or qt.conf at the bottom of the file. Paste all `addnode=1.2.3.4` lines into the file; this can be copied by pressing the copy addnodes button at the bottom of the list on the webpage.
6. Start Pure and wait for the blockcount to be up to date. The current blockcount can be found by looking at the [block explorer](#pure-block-explorer)
7. Once block count is up to date in Pure go to the top menu bar and select Help -> Debug Window -> Console, run `repairwallet` at the bottom input box. 
8. Close Pure all the way; shut it down. Start Pure.

#### Remove user from VSP
The following example uses the username `mn9`.  

    sudo su
    DELUSR='mn9'
    systemctl disable ${DELUSR} -f --now 
    rm -f /etc/systemd/system/${DELUSR}.service
    userdel -rfRZ ${DELUSR}
    systemctl daemon-reload

#### Windows Guide
https://masternodeguides.com/setup-pure-masternode-pure-masternodes/

#### Pure Website
https://purealt.org/

#### Coinmarketcap
https://coinmarketcap.com/currencies/pure/

#### Where Can I buy Pure?
https://www.coinexchange.io/market/PURE/BTC?r=f0466c8f  
https://wallet.crypto-bridge.org/market/BRIDGE.PURE_BRIDGE.BTC?r=798254

#### 3rd party Monitoring service  
https://masternodes.online/monitoring/  
https://masternodeonline.com/  
 
#### Pure Block Explorer  
http://purexplorer.dynu.net/  
http://104.200.67.171:12312/  

#### List of very cheap VPS - Use at your own risk!  
http://subnetlabs.com/billing/aff.php?aff=455&pid=37 - $12 a year, takes hours to provision.  
https://vrtz.net/type/yearly/ - List of all providers.  
https://aws.amazon.com/free/ - 1 year of free hosting; EC2 is hard to setup.

#### Android wallet
https://drive.google.com/file/d/1s45HUhet1Pl9K0TlBHuUQtH8rIB3Pg6L/view  
Source: https://twitter.com/purealtcoin/status/933272382449635328

---
---

# Appendix

## Useful commands to run as root on your VPS:

Switch user to root (do this first):  
`sudo su`  

View top of config file  
`head -20 /home/mn1/.pure/pure.conf`  

Check version:  
`su - mn1 -c '~/pure/pured getinfo'`  

Check if mn has been started remotely:  
`su - mn1 -c '~/pure/pured masternode debug'`  

Check mn status (9 is up and running):  
`su - mn1 -c '~/pure/pured masternode status'`  
This almost always says "Could not find suitable coins!"  
Ignore the warning here and pay attention to the number.  

Start daemon:  
`su - mn1 -c '~/pure/pured --daemon'`  

Stop daemon:   
`su - mn1 -c '~/pure/pured stop'`  

Get connection count:  
`su - mn1 -c '~/pure/pured getconnectioncount'`  

Get block count:  
`su - mn1 -c '~/pure/pured getblockcount'`  

systemctl commands  
`systemctl start mn1`  
`systemctl stop mn1`  
`systemctl restart mn1`  
`systemctl status --no-pager --full mn1`  

---
---

### Upgrade PURE code ###
<details><summary>Click here to read update from github instructions</summary>

This is only needed if the wallet code on github has been updated after you have your mn up and running.  
Run this as root with the pure daemon running to recompile pure and update the running masternodes.
#### `bash -c "$(wget -qO- -o- goo.gl/T6EKiJ)"`
`O` is the letter not the number if you are typing this out.  
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) is highly recommended in order to use copy/paste.  
Once done go to your wallet, unlock it, and start the mn again.

You can view the script here https://goo.gl/T6EKiJ

</details>
  
---
---

## Stake on Linux VPS ##
<details><summary>Click here to read how to stake on linux instructions</summary>

This is experimental but in theory this should work.  
1. Stop pured  
2. Copy your wallet.dat to ~/.pure/wallet.dat  
3. `chmod 777 ~/.pure/wallet.dat`
4. Start pured  
5. run `pured  walletpassphrase "password" 999999999 false`  
replace password with your wallet's password.  

</details>

---
---

# Pure Tip Address #
PR1y6XspcWptRUxKVpCkQjmpgRUSAPjox9



---
---
# Expert Mode
<details><summary>Click here to read the Expert mode way</summary>


Disable root login via SSH.  
#### `bash <(curl -s https://gist.githubusercontent.com/mikeytown2/27875cb8b2b4d2d8798de18f51e4e9ec/raw/2350fa161b4d83d6eb7939830c895b63980bc80b/createrootuser.sh)`


#### Write down/Copy the new username and password 


Login using the new username and password in a new shell.
Login via ssh root will no longer work.  
#### `sudo su root`  
This will update the system and compile the pure masternode code.
Run code again to add more masternode users.  
#### `bash <(curl -sL https://gist.githubusercontent.com/mikeytown2/edd65c5a13c62f8f9323a3d4e49edba6/raw/pmn.sh)`

---
## Walk through ##
## How to generate private ssh key ##
Download [latest Putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.70-installer.msi) for windows. See [Putty website](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) to learn more.

Open PuTTYgen:  
![PuTTYgen](https://www.ssh.com/s/puttygen-run-479x471-2OQ8dV2Z.png "PuTTYgen")

Click Generate:  
![PuTTYgen Generate](https://www.ssh.com/s/puttygen-generate-putty-ssh-key-479x471-cv40+izP.png "PuTTYgen Generate")

Input key passphrase and confirm passphrase and click save private key:
![PuTTYgen Save](https://www.ssh.com/s/pyttygen-created-ssh-key-479x471-reHlFacl.png "PuTTYgen Save")  
Write down this passphrase, you will be using it. If you forget it you are SOL.

## How to have PuTTY use private ssh key for login ##
Open up PuTTY, on left side under Connection expand SSH and click Auth

Under Private key file for authentication click Browse  
![PuTTY ssh auth](http://www.unixwiz.net/images/putty-openssh-11.gif "PuTTYgen ssh auth")  
Select your ppk file that was just generated.

On the left hand side go back up to the top and select Session  
![PuTTY ssh auth](https://linode.com/docs/assets/putty-configuration-window.png "PuTTYgen ssh auth")  
Paste in the IP of your VPS. Now is a good time to save the session

## Get a VPS from here ##
https://www.vultr.com/?ref=7333199

Once signed up go here https://my.vultr.com/deploy/ 
- 2 select Ubuntu 16.04
- 3 select $2.50
- Click deploy now button

Once deployed (wait 2 minutes) click the Manage button on the right

Under IP click the copy icon  
![copy icon](https://www.materialui.co/materialIcons/content/content_copy_black_144x144.png "copy icon")  
and paste that info the Host Name (or IP address) field. Below under Saved Session type in pure-mn and hit save.

Now click open. Click Yes on the PuTTY Security Alert popup.  
![Security Alert](https://www.ssh.com/s/putty-security-alert-431x298-mqLph86E.png "Security Alert")  

`login as: root`  
`Server refused our key`  

Go back to the vultr manage webpage and under password click the copy icon  
![copy icon](https://www.materialui.co/materialIcons/content/content_copy_black_144x144.png "copy icon")  

Back on the PuTTY screen right click (right click is paste) and press enter to fill in the password. 

`root@x.x.x.x's password:` 

## Make server more secure ##
 Copy this and right click to paste into PuTTY window and press enter.  
`bash <(curl -s https://gist.githubusercontent.com/mikeytown2/27875cb8b2b4d2d8798de18f51e4e9ec/raw/2350fa161b4d83d6eb7939830c895b63980bc80b/createrootuser.sh)`

On the PuTTY Key Generator window under "Public key for pasting into OpenSSH authorized_key file" copy the contents of that box.  
![PuTTYgen Save](https://www.ssh.com/s/pyttygen-created-ssh-key-479x471-reHlFacl.png "PuTTYgen Save")  
In the PuTTY console right click to paste and hit enter.

Copy the user:pass string that is repeated twice; highlight the string via left mouse click and drag, that will copy it.

On the top of the console where the title bar is right click and select duplicate session.
![duplicate session](https://support.cs.umu.se/images/software/putty/puttymenu.png "duplicate session")  

Highlight the username (part before :) from the old PuTTY window, and then in the new Putty Window right click to paste it in.

`login as:` {NEW USER NAME} (Right Click & Enter)  
`Authenticating with public key "rsa-key-XXXXXXXX"`  
`Passphrase for key "rsa-key-XXXXXXXX":`  (type in the password that you set in PuTTYgen)    
`Further authentication required `  

In the old console highlight the password (part after :)  
`{NEW USER NAME}@x.x.x.x's password:` (Right Click & Enter)  

### If this doesn't work ###
If you didn't follow the directions exactly you can reset your VPS by going to https://my.vultr.com/ and on the right side click ... and select Server Reinstall. Also make sure that you have PuTTY setup to use your private key for login.

## Install Masternode on VPS ##
Run this in the new console (Where you had to input 2 passwords to login)  
`sudo su root`  
In the old console highlight the password (part after :) and then paste it in (right click).  
Your prompt should now look like `root@vultr:/home/XXXXXXXXXX#`

Copy this and paste it in (right click enter)  
#### `bash <(curl -sL https://gist.githubusercontent.com/mikeytown2/edd65c5a13c62f8f9323a3d4e49edba6/raw/pmn.sh)`

Press enter for the new username `mn1`  
Press enter for the default IP Address  

Wait 40 minutes. Once done this will output what's needed for the pure wallet to get the masternode running from the VPS side.

## Quick Summery ##
You need to have your ppk file, password for that private key, new username and password all kept in a safe place. This is all needed to log back into this VPS.


</details>
