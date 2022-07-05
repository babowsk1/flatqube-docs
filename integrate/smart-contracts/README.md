---
description: >-
  Learn about the smart contracts used in FlatQube and how to integrate with
  them.
---

# Smart contracts

FlatQube is a smart contract system consisting of many libraries.

These smart contracts define the logic for managing DEX Pools, managing liquidity inside the pairs pool, deploying and updating new pairs and accounts, swapping EVERs to other TIP-3 tokens or TIP-3 tokens to EVER, creating vault and much more which is described sections below.

**Libraries list:**

* **DexErrors** - contains codes with all the errors and their meaning.
* **DexGas** - contains value for different types of operations.
* **DexOperationTypes** - contains codes of all different dex operation types.
* **DexPlatformTypes** - contains codes for different platform types.
* **EverToTip3Errors** - contains codes with all the errors specifically related to EverToTip3 swap.
* **EverToTip3Gas** - contains gas values for different types of operations specifically related to EverToTip3 contract.
* **EverToTip3OperationStatus** - contains code values that represent operation status in EverToTip3 contract.
* **TokenFactoryErrors** - contains codes with all the errors related to the token factory.

{% embed url="https://github.com/broxus/ton-dex/tree/master/contracts" %}
