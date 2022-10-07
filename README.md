This repository was forked from Kralverde's https://github.com/kralverde/ravencoin-stratum-proxy

Note: Preliminary version which works. But the hard-coded minerdevfund address will need to be changed as required by Evrmore

# evrmore-stratum-proxy
Allows you to mine directly to your own local wallet/node with any mining software that uses the stratum protocol.

If you are a windows user and are not familiar with python, a walk-through and auto installer is avaliable for a (hopefully) easy install. See [here](#windows).

## *Important Note*
This is BETA software mainly tested on test-net, but has been confirmed to work on mainnet. (First known coinbase thanks to @pdath: https://rvn.cryptoscope.io/api/getrawtransaction/?txid=abf95dd29ac6732b5ff068bbc1063ef734268a2f04459f3be8ce2f5ea2d1e529&decode=1 can check by putting the vin0 coinbase into a hex->ascii converter).

## *Important Note 2*
This is not pool software and is meant for solo-mining. All proceeds go to the address of the first miner that connects.

## *Important Note 3*
Mining software will only send a share when it has found a block. No shares for long periods of time is normal behavior.

## Table of Contents  
- [Setup](#setup)
- [Node Requirements](#node)
- [Usage](#usage)
- [Help](#help)

<a name="setup"/>

## Setup:

1. Requires python 3.8+
2. Run `python3 -m pip install -r requirements.txt`
  - Note that the pysha3 module will need to be compiled so you need some kind of C compiler installed. Alternatively, a precompiled `.whl` is avaliable in `windows/python_modules`.

<a name="windows"/>

#### For Windows:
A bat file is avaliable to auto install python and dependencies and generate another bat file to run the stratum.
1. Ensure your node is configured [as required](#node).
2. (Re)start your node (the qt wallet works).
3. Download this repo (https://github.com/EvrmoreOrg/evrmore-stratum-proxy/archive/refs/heads/master.zip)
4. Unzip the downloaded file
5. Open the unzipped folder
6. Open the `windows` folder
7. Double-click `generate_bat.bat`
8. After `generate_bat.bat` completes with no errors, go back to the previous folder.
9. Double-click `run.bat` to run the stratum converter.

<a name="node"/>

## Node Requirements:

Requires the following `evrmore.conf` options:
```
server=1
rpcuser=my_username
rpcpassword=my_password
rpcallowip=127.0.0.1
```
On *nix OS's this file is located at `~/.evrmore` by default. On windows, this file is located at `%appdata%\roaming\Evrmore`.

You may need to create the `evrmore.conf` file and add those lines if it does not exist.

For testnet you can add `testnet=1` to your `evrmore.conf`

note:
- Default Mainnet rpcport = `8819`
- Default Testnet rpcport = `18819`

Make sure you configure the rpcport on `stratum-converter.py` accordingly.

<a name="usage"/>

## Usage:
The stratum converter uses the following flags `python stratum-converter.py Port_for_miner Ip_of_node Rpc_username Rpc_password Rpc_port Allow_external_connections Is_testnet(optional)` 

With this in mind we can run **testnet** from a local node with a local miner:
```
python3 stratum-converter.py 54325 localhost my_username my_password 18819 false true
```
And for a local node on **mainnet** with an external miner:
```
python3 stratum-converter.py 54325 localhost my_username my_password 8819 true
```

Connect to it with your miner of choise:

| status | miner | example |
| - | - | - |
| :heavy_check_mark: Works | evrprogpowminer | evrprogpowminer -P stratum+tcp://YOUR_WALLET_ADDRESS.worker@PROXY_IP:54325 |

<a name="help"/>

## Help:
@kralverde#0550 is avaliable on the community ravencoin server (https://discord.gg/jn6uhur)
