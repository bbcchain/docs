---
description: This tutorial explains how to transfer
---

# Bridge between Butane chain & Ethereum

The bridge, based on POA's bridge implementation, is used to transfer Butane tokens between the Butane chain and the Ethereum network.

Tokens sent to the respective bridge contract on one network \(whether it's Butane or Ethereum\) are "locked" in the bridge, "unlocked" on the other network bridge and transferred to the sender.

The validators of the bridge on both network are the Butane chain validators. This means that validators, as part of their governance responsibilities, also need to validate bridge transactions and therefore hold Butane tokens to "approve" bridge transactions on Butane chain and hold ETH to "approve" transactions on Ethereum.

Each bridge transaction must be approved by a majority \(over 50%\) of the validators in order to be processed successfully.

The bridge contracts are deployed on both networks, and bridge oracle processes run on each validators machine as part of the validator deployment stack.

Besides the transfer of Butane tokens between the two networks, the bridge is also responsible for network core functionality events:

**Mint block reward distributed on the Butane chain on Ethereum**

Each cycle the total block reward distributed on Butane chain is minted on Ethereum and locked on the bridge contract.

This works by listening to the \`RewardedOnCycle\` event emitted by the BlockReward contract on Butane chain, waiting for all bridge validators on Butane chain to sign it, and eventually sending a transaction to mint on Ethereum \(by the last signing validator\).

**Update Butane chain validators on Ethereum**

Each cycle the Butane chain validators are selected from a random snapshot of pending validators.

Those validators, being also the bridge validators, need to be updated on Ethereum as well.

This works by listening to the \`InitiateChange\` event emitted by the Consensus contract on Butane chain, waiting for all bridge validators on Butane chain to sign it, and eventually sending a transaction to set the bridge validators on Ethereum \(by the last signing validator\).

{% hint style="info" %}
Butane chain bridge - [0xd617774b9708F79187Dc7F03D3Bdce0a623F6988](https://bbcscan.io/address/0xd617774b9708f79187dc7f03d3bdce0a623f6988)

Ethereum bridge - [0xC226f0AeA65942AB94434997bd0B98b30FF1d53d](https://etherscan.io/address/0xC226f0AeA65942AB94434997bd0B98b30FF1d53d)

Butane token on Ethereum - [0x970B9bB2C0444F5E81e9d0eFb84C8ccdcdcAf84d](https://etherscan.io/token/0x970B9bB2C0444F5E81e9d0eFb84C8ccdcdcAf84d)
{% endhint %}

**Using the bridge**

**Transfering from Ethereum mainnet to Fusenet** - send your erc20 Butane tokens to the Ethereum bridge for them to be released from the Butane chain bridge and be avaliable in your native Butane wallet.

**Transfering from Fusenet to Ethereum mainnet** - send your Native Butane tokens to the Butane chain bridge for them to be released from the mainnet bridge and be avaliable in your Mainnet wallet. _Note: there is currently a minimum transfer amount of 30000 Butane across the Butane chain bridge_

