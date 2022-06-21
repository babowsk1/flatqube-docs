---
description: Learn how LP tokens are minted against the provided liquidity
---

# Calculate the amount of LP tokens

## Initial supply

When you create a new liquidity pool and deposit liquidity in it, you get the initial amount of LP tokens used as a benchmark for all consequent supplies. Let's look at an example to understand the initial minting process better.

Imagine you are creating a pool of 1,000,000 APPLE and 200 CUCUMBER tokens, which have the following precision (number of digital places after the comma):

* APPLE - 6 digits (0.000 000)
* CUCUMBER - 12 digits (0.000 000 000 000)

As Everscale smart contracts operate in integer numbers, they perceive the number of tokens as one big number joining together the integer part and the fraction up to the precision. In other words, 1 APPLE is saved as 1,000,000 in the smart contract, whereas 1 CUCUMBER token is 1,000,000,000,000.

So in our example, 1,000,000 APPLE tokens turn into 1,000,000,000,000 in smart contract memory, and 200 CUCUMBERs into 200,000,000,000,000.

Next, the contract takes the biggest number of those two (i.e., 200,000,000,000,000) and divides it by LP-token precision (9 digits) to issue LP tokens. It means that at the end of the pool creation, you will get 200,000 FLATQUBE-LP-APPLE-CUCUMBER tokens.

## Subsequent supplies

All subsequent supplies operate on the proportion of newly provided liquidity compared to (a) the current liquidity level in the pool and (b) the total supply of LP tokens.

Let's imagine we decided to add 200,000 APPLE and 40 CUCUMBER tokens.

In such a case, the contract will calculate the amount of LP tokens to mint following this formula:

$$
LP_{issue}=LP_{current} × max(\frac{SupplyLeft_{new}}{SupplyLeft_{old}},\frac{SupplyRight_{new}}{SupplyRight_{old}})
$$

So in our case, it will be:

$$
LP_{issue}=200,000\times max\big(\frac{200,000,000,000}{1,000,000,000,000},\frac{40,000,000,000,000}{200,000,000,000,000}\big)=50,000
$$

The total LP-token supply in our example will result in:

$$
LP_{new}=LP_{old}+LP_{issue}=200,000+50,000=250,000
$$

{% hint style="warning" %}
Please note that the balance between tokens in the pool will change after each swap. So you will need to provide a different number of pool tokens to get the same number of LP-tokens.
{% endhint %}
