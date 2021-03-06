# ATC masternode install tutorial

## Description

This tutorial uses the 5werk/ATCd docker container to setup a ATC masternode. If you don't know docker, check out their website.

Follows this 6 steps to host your own masternode:

    0. Prerequisites
    1. Client: Prepare a wallet
    2. Server: Install docker
    3. Server: Create the ATC.conf
    4. Server: Install and run 5werk/ATCd
    5. Client: Unlock the wallet
    6. Server: Upgrade the ATC server periodically

## 0. Prerequisites
You need to have root access to a **64bit linux server with Kernel 3.8+** (requirement to run docker) which ideally has a static public ip address in order to be a reliable ATC masternode.
Additionally you need to own at least **100,000 ATC** coins for operating a masternode. Since ATC masternodes allow a hot/cold wallet setup, you don't need to put a wallet with coins on the server.

For this tutorial you should install **curl**, if its not installed already (like on ubuntu). On debian for example use the following command:
```bash
sudo apt-get install curl
```

## 1. Client: Prepare a wallet
Please install the latest version of ATC-qt on your local computer. Download the executable file from the [ATC]
### Always encrypt and backup your wallet
Make sure your wallet is encrypted with `Settings > Encrypt Wallet`.
Save the password. Now export your wallet with `File > Backup Wallet` to
a safe location.

### Generate a masterprivkey and transfer 100,000 ATC
When your block-chain is synchronised you can create a masternode private key. Open the debug console at `Help > Debug Window > Console` and type following command:

```bash
masternode genkey
```

Save the output (long string of numbers and letters) in a textfile. You will need the key during **step 3**.

Now create a new account address with the following command:
```bash
getaccountaddress "My Masternode"
```
Now transfer exact 100,000 ATC to this newly generated address using the `Send > Pay To:` Field. Make sure the field below reads `Label: My Masternode`.

## 2. Server: Install docker
Check out the in order to understand how to install docker on the specific linux distribution you are running.

The install command for ubuntu is as follows:

```bash
curl -sSL https://get.docker.com/ubuntu/ | sudo sh
```

For debian, see [installation instructions](https://docs.docker.com/installation/debian/).

## 3. Server: Create the ATC.conf
Choose a folder where you want to house the ATC blockchain and the server config file. In this setup we use `/var/ATC`.

*Careful: this command overwrites the file /var/ATC/ATC.conf*

```bash
sudo sh -c 'mkdir -p /var/ATC && curl -
```

You can now edit the `ATC.conf` file (still with root permissions) using your favourite editor vim:
```bash
sudo vim /var/ATC/ATC.conf
```

Make sure the `ATC.conf` is filled out with the masternodeprivkey you obtained during the first step of this tutorial. Change at least the following 3 entries of the template config file:

```config
masternode=1
masternodeprivkey=[FILL IN FROM ABOVE]
rpcpassword=[super secure random password with 30 or more characters. You probably never need to use it]
```

Since we set the permissions of the config file to owner read-only you have to save with
`<ESC>:wq!` in vim (the root user always has write permissions).

You can easily generate a random password using the following
command or a multitude of [other methods](http://www.howtogeek.com/howto/30184/10-ways-to-generate-a-random-password-from-the-command-line/):
```bash
date | md5sum
```
 We recommend you install the script in `/usr/local/bin/` as follows:

```bash 
```

Change the default paths in the script, if you don't use `/var/ATC`. If the script is configured to your likings install and run the **5werk/ATCd** docker image like this:
```bash
sudo ATC-server.sh install
```
This command creates a running docker instance named **ATC-server**. Check out the status of the service with:

```bash
sudo docker ps -a
```

When the ATC service started properly it begins to download the blockchain. You can check the current status with this command:

```bash
sudo docker exec ATC-server ATC-cli getinfo
```

Later you can use all the docker standard commands like `sudo docker restart ATC-server` to restart the service. If the service isn't running use this command to investigate: `sudo docker logs ATC-server`.

## 5. Client: Unlock the wallet

For the next step the server needs to complete to download the blockchain first. When the download finished you can go on your local pc and stop your **local** client. Open your **local** `ATC.conf` file. Typical paths where you can find it are the following:

Operating System  |Path                                          |
------------------|----------------------------------------------|
Windows 7/8       |C:\Users\YourUserName\Appdata\Roaming\ATC  |
Mac OSX           |~/Library/Application Support/ATC/           |
Linux             |~/.ATC/                                      |

Add the following config options:
```config
server=1
addnode=23.23.186.131
masternode=1
masternodeprivkey=[FILL IN FROM ABOVE]
masternodeaddr=[ip address of your server]:9999
```

Now start the client and open the console at `Help > Debug Window > Console`. To authentificate your remote server type the following into the console:
```bash
masternode start [your wallet password]
```
If successful, you will see a message like *"successfully started masternode"*. If you have problems, run `sudo tail -f /var/ATC/debug.log`.

***Congratulations! You successfully setup your ATC masternode!***

## 6. Server: Upgrade the ATC server periodically
Check periodically if the ATC developers upgraded the ATC runtime. We will try to keep the docker image up-to-date. The upgrade process for you is relatively simple. Just run:

```bash
sudo ATC-server.sh upgrade
```

If you have problems with the latest image you can always downgrade to a prior ATC version (if it is still supported) using the following command:
```bash
sudo ATC-server.sh install-version Giga-X 1.0192.201
```
* * *
Feel free to open Github issues for comments.

