# Pool economics

Each FlatQube liquidity pool is a trading venue for a [pair ](../tokens/interface/token-page/pairs.md)of TIP-3.1 tokens.\
When a [pool contract is created](../pairs/how-to/create-new-pair.md), its balances for each token are 0; in order for the pool to begin facilitating trades, someone must seed it with an initial deposit for each token.\
This first liquidity provider is the one who sets the initial price of the pool. They are incentivized to deposit an equal _value_ of both tokens into the pool. To understand why, consider a case where the first liquidity provider deposits tokens at a ratio different from the current market rate. This immediately creates a profitable arbitrage opportunity, which is likely to be exploited by an external party.

When other liquidity providers add to an existing pool, they must deposit pair tokens proportional to the current price. If they don’t, the liquidity they added is at risk of being arbitraged as well. If they believe the current price is not correct, they may arbitrage it to the level they desire, and add liquidity at that price.

As we’ve mentioned, a liquidity pool is a bunch of funds deposited into a smart contract by liquidity providers. When you’re executing a trade on FlatQube you’re executing a trade against the liquidity in the liquidity pool. For the buyer to buy, there doesn’t need to be a seller at that particular moment, only sufficient liquidity in the pool.

When you’re buying a coin on FlatQube, there isn’t a seller on the other side in the traditional sense. Instead, your activity is managed by the algorithm that governs what happens in the pool. In addition, pricing is also determined by this algorithm based on the trades that happen in the pool.

### LP tokens

Whenever liquidity is [deposited ](how-to/add-liquidity.md)into a pool, unique tokens known as **LP tokens** are minted and sent to the provider's address. These tokens represent a given liquidity provider's contribution to a pool. The proportion of the pool's liquidity provided determines the number of liquidity tokens the provider receives.\
\
Whenever a trade occurs, a 0.3% [liquidity provider fee](../swap/concepts/fees.md) is charged to the transaction sender. This fee is distributed _pro-rata_ to all LPs in the pool upon completion of the swap.

To retrieve the underlying liquidity, plus any fees accrued, liquidity providers must ["burn" their liquidity tokens](how-to/withdraw-liquidity.md), effectively exchanging them for their portion of the liquidity pool, plus the proportional fee allocation.

As liquidity tokens are themselves tradable assets, liquidity providers may sell, transfer, or otherwise use their liquidity tokens in any way they see fit.

Since liquidity is very important, FlatQube has a special interface to encourage liquidity providers - [**Farming**](../farming/). You can lock your **LP tokens** in the appropriate farming pools for rewards.

\\
