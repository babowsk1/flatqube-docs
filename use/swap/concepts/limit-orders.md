# Limit orders

One of its key features on the FlatQube is the implementation of Limit orders, which provides traders with increased control and flexibility over their trades.

### **Understanding Swaps**

In the context of a decentralized exchange (DEX), a "swap" refers to the process of exchanging one token for another. Traditionally, through FlatQube's standard Swap interface, this is done at the current market price, which is determined by the balance of supply and demand in the token pair's liquidity pool. Essentially, you are "swapping" one token for another.

Automated Market Makers (AMMs) facilitate these swaps. AMMs are smart contracts that create a liquidity pool of two tokens. They determine the price of tokens based on the ratio of the tokens in the pool. However, these swaps only happen at the prevailing market price, providing less control over your trades.

### **Limit Orders: A Step Beyond Traditional Swaps**

A Limit order represents a significant enhancement to standard swaps. This type of order enables you to stipulate the price at which you aim to buy or sell a specific quantity of a token. You're no longer tied to the prevailing market price. Instead, you can place an order that executes only when the token's price matches your predetermined value.

This feature is particularly useful in volatile markets, where token prices can fluctuate rapidly. By setting a limit order, you can manage risk as the order will only be executed when the token reaches your specified price.

In practice, as a user, you simply set a price for your order and wait. Once the market price matches your specified price, the order can be executed. It's important to note that while your order can be fulfilled by another user's actions, other traders do not have the ability to intentionally choose and fulfill your specific order. The fulfillment of your order is dictated by the market activities and mechanisms within the DEX, which decide whether an AMM or another user's order matches your specified price.

### **How Limit Orders Work**

When you place a limit order on FlatQube, there are three mechanisms through which the order can be executed:

1. **P2P Execution:** Another trader can manually accept your order and execute it, either fully or partially.
2. **Order Matching:** If there is an existing order that matches yours in terms of price and quantity, the DEX automatically executes both orders, either fully or partially.
3. **AMM Execution:** When the market price reaches your set price, the DEX automatically executes your order by initiating a swap in the pair you have selected.

The automatic execution methods (Order Matching and AMM Execution) come with two modes provided in smart contracts:

* The backend triggers the match
* Another trader triggers a match for the difference as a reward. This acts as a fallback to ensure decentralization in case the backend is unavailable.

### **Monitoring Your Orders**

Once created, your order is added to the order table located at the bottom of the Swap page. The order remains there until it is either fully executed or cancelled by you, the creator. This allows for a full audit trail of all placed orders.

Limit orders enhance your trading experience on FlatQube by providing greater control and flexibility in your Web3 trading decisions. They also facilitate increased interaction with other traders on the Everscale blockchain. Dive into the world of decentralized trading with FlatQube limit orders!
