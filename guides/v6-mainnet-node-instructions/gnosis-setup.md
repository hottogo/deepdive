---
description: 'Last updated: 2024-02-02'
---

# Gnosis setup

#### The guide below is for running a node on Gnosis chain only.

{% hint style="info" %}
As of February 2024, Gnosis chain is the only chain that supports delegated staking. Delegated staking is expected to come on NeuroWebAI shortly after.
{% endhint %}

## Step 1 - Add Gnosis Network to MetaMask

Begin by adding the Gnosis network to your Metamask extension by either connecting MetaMask to this [**link** ](https://chainlist.org/?search=gnosis)or manually

| Network name        | Gnosis                                           |
| ------------------- | ------------------------------------------------ |
| **RPC URL**         | [https://1rpc.io/gnosis](https://1rpc.io/gnosis) |
| **Chain ID**        | 100                                              |
| **Currency symbol** | XDAI                                             |

Add xTRAC on MetaMask by importing the contract address below

```
0xEddd81E0792E764501AaE206EB432399a0268DB5
```

## Step 2 - Fund your wallet

Begin by obtaining xDAI for operations on Gnosis chain through their [f**aucet**](https://www.gnosisfaucet.com/).

Gnosis is EVM compatible. Therefore, you can use your Ethereum wallet on MetaMask or Ledger for all operations.

If you want to delegate to your own node, bridge your ERC-20 TRAC from Ethereum to Gnosis by using the [**Omnibridge**](https://omnibridge.gnosischain.com/bridge).

{% hint style="info" %}
A node can be fully operational with delegated stake only as long as the total stake amount is 50k TRAC or above.
{% endhint %}

## Step 3 - Install your node

In order to deploy your OriginTrail V6 node on Gnosis, you will need a Linux (Ubuntu) server with the following minimum recommended hardware:

* **4GB RAM**
* **2CPUs**
* **50GB HDD space**

{% hint style="warning" %}
Log into the server as root. You **cannot** use sudo and run this script.
{% endhint %}

Gather the following information:

| Value                          | Description                                                                  |
| ------------------------------ | ---------------------------------------------------------------------------- |
| EVM\_OPERATIONAL\_WALLET       | <p>Public address of your operational wallet<br>Example: MetaMask wallet</p> |
| EVM\_OPERATIONAL\_PRIVATE\_KEY | Private key of your operational wallet                                       |
| EVM\_MANAGEMENT\_WALLET        | <p>Public address of your management wallet<br>Example: Ledger wallet</p>    |
| SHARES\_TOKEN\_NAME            | Your choice of token name                                                    |
| SHARES\_TOKEN\_SYMBOL          | The token symbol of your token name                                          |

**Run the one-liner installer script and select the appropriate prompts**

```
cd /root/ && curl -k -o https://raw.githubusercontent.com/OriginTrail/ot-node/v6/develop/installer/installer.sh && chmod +x installer.sh && ./installer.shYou must choose a SQL password for the installer to work. Do not leave that field empty.
```

{% hint style="danger" %}
You must choose an SQL password for the installer to work. Do not leave that field empty.
{% endhint %}

{% hint style="info" %}
**Reminder**:

In order to use aliases to quickly check node logs, start/stop/restart node, change node config, you must execute the following script after the installation:

\
source \~/.bashrc

Once the sourcing is done, try the following:\
otnode-logs

otnode-start

otnode-stop

otnode-restart

otnode-config
{% endhint %}

#### You have now successfully completed your node installation! You can check the logs by using the alias otnode-logs.

## Step 4 - Set node ask

The default ask is set to 0.01 in the script below. Please change it to your desired ask price.

```
npm -C /root/ot-node/current run set-ask -- --rpcEndpoint=https://astrosat-parachain-rpc.origin-trail.network/ --ask=0.01 --privateKey=$(jq -r '.modules.blockchain.implementation.otp.config.evmOperationalWalletPrivateKey' /root/ot-node/.origintrail_noderc) --hubContractAddress=0x5fA7916c48Fe6D5F1738d12Ad234b78c90B4cAdA
```

## Step 5 - Add stake

Visit [**Houston**](https://houston.origintrail.io/login) **and connect your admin wallet. Head to Service Tokenomics and follow the on screen instructions to set up node operator fee, node ask and node stake!**

**You can then visit the**[ **staking dashboard**](https://dkg.origintrail.io/staking) to find your node.

Done!
