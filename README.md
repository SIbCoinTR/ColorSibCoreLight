## ColorSibCore Light 


ColorSibCore light  is an open source colored coin wallet compatible for exchange and basic level developer . It supports two modes: a command line interface, and a JSON/RPC server. The command line interface is suitable for managing a local wallet without going through any third-party service. The JSON/RPC interface is suitable for server-side implementations of colored coins and programmatic colored coins wallet management.
## Requirements

The following items are required to run ColorSibCore in the default mode:

-   [Python 3.4](https://www.python.org/downloads/)
-   The following Python packages: , [python-bitcoinlib](https://github.com/petertodd/python-bitcoinlib), [aiohttp](https://github.com/KeepSafe/aiohttp)
-   An operational [Sibcoin Core](https://github.com/ivansib/sibcoin) wallet with JSON/RPC enabled and full transaction index

## Installation

Clone the source code from GitHub:

    $ git clone https://github.com/SIbCoinTR/ColorSibCoreLight.git

**Update the requirements:** 

    $ cd ColorSibCoreLight
    $ pip3 install --upgrade -r requirements.txt
    $ pip3 install aiohttp

## Configuration

Make sure you have a SibCoin Core server running, with the following arguments: -adreessindex=1 txindex=1 -server=1. You may need to have a username and password configured in the configuration file for Sibcoin Core (Sibcoin.conf).

All the configuration for ColorSibCore is done though the config.ini file:

    [general]
    
         #Defines what provider to use to retrieve information from the Blockchain 
    
    blockchain-provider=sibcoind
    
    [sibcoind]
    
    # Replace username, password and port with the username, password and port for Sibcoin Core
    
    # The default port is 8332 in MainNet and 18332 in TestNet
    
    rpcurl=http://<username>:<password>@localhost:<port>
    
    [environment]
    
    dust-limit=600
    
    default-fees=10000
    
    [cache]
    
    # Path of the cache file (use :memory: to disable)
    
    path=cache.db
    
    [rpc]
    
    # The port on which to expose the ColorSibCore RPC interface
    
    port=8080

## Usage

The general syntax for executing ColorSibCore is the following:

    python colorcore.py <command> <arguments>

All the commands are documented. Use the following command to show the documentation:

    python colorcore.py --help

The currently supported commands are the following:

-   **getbalance**: Returns the balance in both sibcoin and colored coin assets for all of the addresses available in your Sibcoin Core wallet.
-   **listunspent**: Returns an array of unspent transaction outputs, augmented with the asset ID and quantity of each output.
-   **sendsibcoin**: Creates a transaction for sending sibcoins from an address to another.
-   **sendasset**: Creates a transaction for sending an asset from an address to another.

## RPC server

Use the following command to start the RPC server:

    python colorcore.py server

ColorSibCore will then start listening on the port specified in the configuration file.

To call the RPC server, issue a HTTP POST request to`` http://localhost <port>/<operation>`` The list of valid operations is the same as the list of commands available via command line.

 **Get your balance**
 -----

Getting the balance of the wallet stored on the Sibcoin Core instance can be done by using the following command:

    python colorcore.py getbalance

 Optional arguments:

| Parameter | Description |
|--|--|
| `--help`  | show this help message and exit|
| `--address`  | [ADDRESS] Obtain the balance of this address only, or all addresses if unspecified|
|`--minconf`| [MINCONF] The minimum number of confirmations (inclusive)|
|`--maxconf`| [MAXCONF] The maximum number of confirmations (inclusive)|
|`--txformat`| [TXFORMAT] Format of transactions if a transaction is returned ('raw' or 'json')|



**Get your unspent list**
---

Use the sendasset operation to send an asset to another address:

    python colorcore.py listunspent

Optional arguments:

| Parameter | Description |
|--|--|
| `--help`  | show this help message and exit|
| `--address`  | [ADDRESS] Obtain the balance of this address only, or all addresses if unspecified|
|`--minconf`| [MINCONF] The minimum number of confirmations (inclusive)|
|`--maxconf`| [MAXCONF] The maximum number of confirmations (inclusive)|
|`--txformat`| [TXFORMAT] Format of transactions if a transaction is returned ('raw' or 'json')|


**Send an asset**
--
Use the sendasset operation to send an asset to another address:

    python colorcore.py sendasset <from> <asset> <quantity> <to>

Positional arguments:
 


| Parameter | Description |
|--|--|
| address| The address to send the asset from |
|asset| The asset ID identifying the asset to send |
|amount| The amount of asset units to send |
|to| The address to send the asset to|



Optional arguments:

| Parameter | Description |
|--|--|
|`--help`| show this help message and exit|
|`--metadata`| [METADATA] The metadata to embed in the transaction|
|`--fees` |[FEES] The fees in ivan for the transaction|
|`--mode`| [MODE] 'broadcast' (default) for signing and broadcasting the transaction, 'signed' for signing the transaction without broadcasting, 'unsigned' for getting the raw unsigned transaction without broadcasting|
|`--txformat` |[TXFORMAT] Format of transactions if a transaction is returned ('raw' or 'json')|


**Send an Sibcoin**
--
Use the sendasset operation to send an asset to another address:

    python colorcore.py sendsibcoin <from> < amount> <to>


Positional arguments:

| Parameter | Description |
|--|--|
|address| The address to send the sibcoin from amount  The amount of ivan to send|
|to|  The address to send the sibcoin to|

Optional arguments:

| Parameter | Description |
|--|--|
|`--help`| show this help message and exit|
|`--fees`| [FEES] The fees in ivan for the transaction|
|`--mode`| [MODE] 'broadcast' (default) for signing and broadcasting the transaction, 'signed' for signing the transaction without broadcasting, 'unsigned' for getting the raw unsigned transaction without broadcasting|
|`--txformat` |[TXFORMAT] Format of transactions if a transaction is returned ('raw' or 'json')







