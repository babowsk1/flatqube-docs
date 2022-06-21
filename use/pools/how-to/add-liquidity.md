# Add liquidity

Please note that this section assumes that you have already provided liquidity to the required pool. Otherwise, the process will be different - go to the [**new position page**](create-new-position.md).

## Simple liquidity provision

To add tokens to an existing position, go to the [Pools section](../), then go to the [page of the desired pool](../interface/pool-page/) by clicking on the appropriate pair and clicking <mark style="color:red;">**Add Liquidity**</mark>.

After that, you will be taken to the page for adding liquidity to the pool.

![](<../../../.gitbook/assets/image (177).png>)

On this page, you can add liquidty to the pool of this pair.\
\
Recall that you do not need to have both tokens in equal proportion on your balance, since FlatQube has an automatic exchange function that allows you to provide [**one-sided liquidity**](add-liquidity.md#one-sided-liquidity-provision).

#### Adding liquidity (using the WEVER/USDC pair as an example)

To get started, enter the amount of tokens you wish to **add to the pool**.\
You can enter the amount of either the left or right tokens, and the required amount of the second token will be calculated automatically at the current FlatQube rate.

![](<../../../.gitbook/assets/image (52).png>)

After entering the amount, you will see how much your [**Pool share**](../pool-economics.md) will change, as well as the ratio of the price of tokens.

Now you need to deposit tokens. Click Deposit and confirm the transaction in EVER Wallet.

![](<../../../.gitbook/assets/image (208).png>)

After a successful deposit of the left token, do the same for the right one:

![](<../../../.gitbook/assets/image (59).png>)

And here we are almost at the finish line - now it is necessary to produce **Supply**.\
This operation will also require confirmation.

![](<../../../.gitbook/assets/image (127).png>)

After you successfully complete the Supply process, you will see a **Supply receipt window.**

Here you will see the current **Pool share** and the percentage by which it was increased by this transaction, as well as the number of received [**LP tokens.**](calculate-the-amount-of-lp-tokens.md)\*\*\*\*

![](<../../../.gitbook/assets/image (124).png>)

## One-sided liquidity provision

FlatQube has an automatic exchange feature that also allows you to provide one-way liquidity.

In order to provide liquidity using only one of the tokens, enable **Auto Exchange** and enter the amount of one of the tokens.

![](<../../../.gitbook/assets/image (104).png>)

The next steps you need to take are identical to those in the [**first example**](add-liquidity.md#adding-liquidity-on-the-example-of-the-wever-usdc-pair), the only difference being that after depositing the token, you will immediately be taken to **Supply**.

![](<../../../.gitbook/assets/image (92).png>)

After you successfully complete the Supply process, you will see a **Supply receipt window.**

Here you will see the current **Pool share** and the percentage by which it was increased by this transaction, as well as the number of received [**LP tokens.**](calculate-the-amount-of-lp-tokens.md)\*\*\*\*

![](<../../../.gitbook/assets/image (58).png>)
