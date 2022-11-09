# veQUBE

## What’s this?

veQUBE (vote-escrowed QUBE) is a virtual asset that only exists on FlatQube. veQUBE cannot be transferred. The only way to obtain veQUBE is by locking QUBE. The maximum lock time is four years. A user’s veQUBE balance will remain constant until the QUBE is unlocked.

## Everscan

To see a transaction on Everscan, all you need to do is go to the [DAO Balance page](../interface/dao-balance.md) and click on any transaction in the deposits or history.

## What’s it for?

QUBE has several key utility tasks:&#x20;

1. Voting in the DAO&#x20;
2. Boosting rewards in farming

To participate in the utility and get the respective benefits, you need to wrap QUBE into veQUBE.

## How is the number of veQube calculated in relation to the amount and period?

`veQUBE = QUBE * (lock time/max lock time)`

With this kind of token distribution, an investor gets 1:1 from a lock time of four years.

You can lock tokens [here](https://app.flatqube.io/dao/balance).

## How much do you get after unlocking?

When the lock time ends, the investor gets their QUBE tokens returned to their wallet. Put simply, the investor gets as many tokens back as they invested. Needless to say, gas has to be paid in EVER for the transaction.

`QUBE = veQUBE * (max lock time/lock time)`

## **Increasing your balance through veQUBE:**

We have used the curve approach**:**

****<img src="../../../.gitbook/assets/image (17) (1).png" alt="" data-size="original">****

Where:

* **Td** – total deposits.&#x20;
* **d** – deposit of the user.

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

* **veBd** – ve-boosted balance.
* **Gd** – total gauge deposits (TVL of a specific pair in the gauge).
* **veQUBE** – number of veQUBE that the user has.
* **TveQUBE** – total circulating supply of veQUBE.

You can read about the formula for boosted farming from LP locking, summation of locks, and examples in the [boosted farming section](boosted-farming.md).

## How often can you vote?

You can only vote once during the voting period.

## Contracts

{% hint style="warning" %}
As soon as these are public, we’ll post them here.
{% endhint %}
