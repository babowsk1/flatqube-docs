---
description: Learn the basics of FlatQube to better understand the underlying processes.
---

# How it works

## Basics

FlatQube is an automated liquidity protocol inspired by the leading market solutions. It is based on a constant product formula and offers a non-custodial, decentralized, censorship-resistant and secure way to provide liquidity and exchange pairs of tokens.

Unlike Uniswap or other Ethereum-based DEXes, FlatQube works on the [Everscale network](https://everscale.network) and benefits from its asynchronous execution, high throughput, and fast finality.

FlatQube is open-source software licensed under [Apache 2.0](https://github.com/broxus/ton-dex/blob/master/LICENSE).

## Liquidity pools

FlatQube operates through a collection of smart contracts, the principal of which, [_the pair_](https://github.com/broxus/ton-dex/blob/master/contracts/DexPair.sol), manages a liquidity pool made up of reserves of two [TIP-3.1 tokens](../tokens/concepts/tokens-we-use.md#tokens-standard).

Anyone can become a liquidity provider (LP) for a pool by depositing an equivalent value of each underlying token in return for pool tokens (LP-tokens). These tokens track pro-rata LP shares of the total reserves and can be redeemed for the underlying assets at any time.

{% hint style="info" %}
See also: [How to calculate the amount of LP tokens](../pools/how-to/calculate-the-amount-of-lp-tokens.md)
{% endhint %}

Unlike other DEXes, due to the peculiarities of Everscale, FlatQube uses an intermediate contract, [_the DEX account_](https://github.com/broxus/ton-dex/blob/master/contracts/DexAccount.sol), to accumulate the position before provision. An LP should deposit both underlying assets to their DEX account to supply liquidity to the pool.

{% hint style="info" %}
FlatQube supports one-sided liquidity provision by automatically exchanging the required part of the provided asset in the pool. [Read more](../pools/how-to/add-liquidity.md#one-sided-liquidity-provision)
{% endhint %}

## The math behind the curtains

Pairs act as automated market makers, standing ready to accept one token for the other as long as the “constant product” formula is preserved. This formula, most simply expressed as `x * y = k`, states that trades must not change the product (`k`) of a pair’s reserve balances (`x` and `y`). Because `k` remains unchanged from the reference frame of a trade, it is often referred to as the _invariant_. This formula has the desirable property that larger trades (relative to reserves) execute at exponentially worse rates than smaller ones.

In practice, FlatQube applies a 0.30% fee to trades, which increases the reserves and, consequently, the invariant. It serves as a deferred profit to LPs, which they get when they burn pool tokens to withdraw their portion of the total reserves.

By design, the relative price of assets changes only through trading, leading to arbitrage opportunities. This mechanism ensures that DEX prices always trend toward a market-clearing price.
