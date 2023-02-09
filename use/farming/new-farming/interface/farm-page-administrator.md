# Farm page (administrator)

This page will show you how to create and manage your own farming pool.

## Create farming pool

Thanks to the FlatQube functionality, you can create your own pools: choose a farming token, a reward, its distribution rate, etc. \
You can also create a farming pool with a [custom pair](../../../pairs/how-to/create-new-pair.md).

To create a farming pool, go to the **Farming** section and select **Create farming pool** at the top right of the page.

<figure><img src="../../../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

In the page that opens, you need to fill in some fields:

1. First, copy the root address of the token that will be used for farming (LP token) and paste this address into the **Farm token root** line.
2. If necessary, check the box next to **Active** [**token boost**](../../concepts/boosted-farming.md). \
   Enter the maximum token lock period as well as the maximum boost ratio.
3. The standard reward token is QUBE, but you can add any other token as a reward. \
   To do this, click **Add reward token** at the bottom left of the page, enter the root address of the token, the [vesting ](../../concepts/vesting.md)period and the [vesting ](../../concepts/vesting.md)ratio.
4. Click **Create pool** and confirm the transaction in the Ever Wallet window that opens.

<figure><img src="../../../../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

Congratulations, you have created your own farming pool!&#x20;

## Find my farming pool

After you create a farming pool, it will automatically be added to your favorites list. \
However, if you go to the main page of the Farming section you probably won't find it there.&#x20;

The thing is that by default, pools with zero balance are not displayed in the general list.&#x20;

To find your pool, click the "Filters" button in the upper right corner and select With low balance. Then you will see your pool in the general list or in the list of favorites.

## Farming pool Management

### Deposit reward tokens&#x20;

If you add any token other than QUBE as a reward for the farming pool, then, you have the opportunity to manually replenish the reward balance with this token.

Recall that QUBE rewards [are added](../../concepts/reward-distribution.md) to the gauge by DAO voting.

1. Go to your farming pool page from the Farming section.
2. At the top of the Pool management block is the Deposit reward tokens block. Enter the number of tokens you want to deposit into the pool and click Deposit.
3. Confirm the transaction in the Ever Wallet window that opens and wait for it to close.
4. Then you will see this transaction in the transaction list at the bottom of the pool page and its Reward balance will change.

<figure><img src="../../../../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>

### Change farming speed

You can change the reward distribution speed for an award token that is not a QUBE.

Recall that for QUBEs, the reward distribution speed is [determined](../../concepts/reward-distribution.md) by voting in the DAO.

1. Go to your pool page from Farming
2. Click on the [⚙️](https://emojipedia.org/gear/) next to the Pool management block.
3. Enter the desired distribution speed, and the date and time when you want the speed to be changed.
4. Click Save changes and confirm the transaction in the Ever Wallet window that opens.

<figure><img src="../../../../.gitbook/assets/image (310).png" alt=""><figcaption></figcaption></figure>

### Close farming pool

You have the ability to manually stop the farming in your pool. \
\
**Note that this action is irreversible!**

1. Go to the farming pool page from the Farming section
2. Click on the gear next to the Pool management block
3. Click on the Danger zone at the top of the window that opens
4. Enter the date and time when the farming ends. At this point, farming will stop and you can collect the remaining Reward tokens.

<figure><img src="../../../../.gitbook/assets/image (332).png" alt=""><figcaption></figcaption></figure>

****
