# Nodemaster

The **Nodemaster** scripts is a collection of utilities to manage, setup and update masternode instances.

I am quite confident this is the single best and almost effortless way to setup masternodes, without bothering too much about the setup part.

If this script helped you in any way, please contribute some feedback. BTC donations also welcome and never forget:

**Have fun, this is crypto after all!**

```
BTC  33ENWZ9RCYBG7nv6ac8KxBUSuQX64Hx3x3
```


Feel free to use my reflink to signup and receive a bonus w/ vultr:
<a href="https://www.vultr.com/?ref=7557642"><img src="https://www.vultr.com/media/banner_2.png" width="468" height="60"></a>


---

**NOTE on the VPS choice for starters**

**Vultr** is highly recommended for this kind of setup. 

---

Comparing with building from source manually, you will benefit from using this script in the following way(s):

* 100% auto-compilation and 99% of configuration on the masternode side of things. It is currently only tested on a vultr VPS but should work almost anywhere where IPv6 addresses are available
* Developed with recent Ubuntu versions in mind, currently only 16.04 is supported
* Installs 1-100 (or more!) masternodes in parallel on one machine, with individual config and data
* Compilation is currently from source for the desired git repo tag (configurable via config files)
  Some security hardening is done, including firewalling and a separate user
* Automatic startup for all masternode daemons
* This script needs to run as root, the masternodes will and should not!
* It's ipv6 enabled, tor/onion will follow

## Installation

SSH to your VPS and clone the Github repository:

```bash
git clone https://github.com/Block-Logic-Technology-Group/Masternode-Script.git vps && cd vps
```

Install & configure your desired master node with options:

```bash
./install.sh -p bltg
```

## Examples for typical script invocation


**Install & configure 4 BLTG masternodes:**

```bash
./install.sh -p bltg -c 4
```

**Update daemon of previously installed BLTG masternodes:**

```bash
./install.sh -p bltg -u
```

**Install 6 BLTG masternodes 

```bash
./install.sh -p bltg -c 6 
```

**Wipe all BLTG masternode data:**

```bash
./install.sh -p bltg -w
```
**once install command has finished
There is still work to do in the configuration templates.
These are located at /etc/masternodes, one per masternode.
Add your masternode private keys now.
eg in /etc/masternodes/bltg_n1.conf

=>  All configuration files are in: /etc/masternodes
=>  All Data directories are in: /var/lib/masternodes

Important: run  /usr/local/bin/activate_masternodes_bltg  as root to activate your nodes.


## Options

The _install.sh_ script support the following parameters:

| Long Option  | Short Option | Values              | description                                                         |
| :----------- | :----------- | ------------------- | ------------------------------------------------------------------- |
| --project    | -p           | project, e.g. "bltg"| shortname for the project                                           |
| --net        | -n           | "4" / "6"           | ip type for masternode. (ipv)6 is default                           |
| --release    | -r           | e.g. "tags/v2.0.0.0"| a specific git tag/branch, defaults to latest tested                |
| --count      | -c           | number              | amount of masternodes to be configured                              |
| --update     | -u           | --                  | update specified masternode daemon, combine with -p flag            |
| --sentinel   | -s           | --                  | install and configure sentinel for node monitoring                  |
| --wipe       | -w           | --                  | uninstall & wipe all related master node data, combine with -p flag |
| --help       | -h           | --                  | print help info                                                     |
| --startnodes | -x           | --                  | starts masternode(s) after installation                             |

## Troubleshooting the masternode on the VPS

If you want to check the status of your masternode, the best way is currently running the cli e.g. for $MUE via

```
/usr/local/bin/bltg-cli -conf=/etc/masternodes/bltg_n1.conf getinfo

{
  "version": 2000000,
  "protocolversion": 70921,
  "walletversion": 61000,
  "balance": 0.00000000,
  "privatesend_balance": 0.00000000,
  "blocks": 300,
  "timeoffset": 0,
  "connections": 5,
  "proxy": "",
  "difficulty": 42882.54964804553,
  "testnet": false,
  "keypoololdest": 1511380627,
  "keypoolsize": 1001,
  "paytxfee": 0.00000000,
  "relayfee": 0.00010000,
  "errors": ""
}
```



## Management script (not yet implemented)

The management script release will follow within the next couple of days.

| command                               | description                                  |
| :------------------------------------ | -------------------------------------------- |
| nodemaster start bltg (all\|number)   | start all or a specific bltg masternode(s)   |
| nodemaster restart bltg (all\|number) | stop all or a specific bltg masternode(s)    |
| nodemaster stop bltg (all\|number)    | restart all or a specific bltg masternode(s) |
| nodemaster cleanup bltg (all\|number) | delete chain data for all bltg masternodes   |
| nodemaster status bltg (all\|number)  | systemd process status for a bltg masternode |
| nodemaster tail bltg (all\|number)    | tail debug logs for a bltg masternode        |


```
