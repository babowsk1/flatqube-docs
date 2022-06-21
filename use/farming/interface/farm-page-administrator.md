---
description: Anyone can create and manage their own farming pool.
---

# Farm page (administrator)

## How to create a farming pool

Go to the Farming section and click Create farming pool in the upper right corner and fill in the required fields:

* Farm token root - the address of the token that users deposit to participate in farming. It can be the address of the LP token of the pair.
* Farm start - the date when farming starts.
* Vesting ratio - percentage of the award that goes to vesting.
* Vesting period - vesting period in seconds.
* Reward token root - the address of the token that users farm. There may be several tokens like this one in a farming pool. Use the Add reward token button.
* Reward per second - ​​farming speed, measured in tokens per second.

Click Create farming pool, confirm the transaction in your EVER Wallet and wait for the pool creation process to complete.

## How to go to the page of the created Farming pool?

1. Go to the [farming section](../).
2. In the upper-right part of the **All pools** block, open the filter menu by clicking on the appropriate button and turn on the **With low balance** filter.
3. Find your pool in the list and go to its page by clicking on it.\
   Here you can immediately add it to your [favorites ](../../pairs/interface/pair-page/add-to-favorites.md)so that it appears on the main Farming section page.

![](<../../../.gitbook/assets/image (57).png>)

## Farming pool management

The page of the farming pool for administrators looks exactly like the page of any other [farming pool](farm-page-user/), but with the addition of some management features:

### Deposit rewards

The administrator of the farming pool can at any time deposit tokens into the pool that will be used to pay rewards.

The administrator has to monitor the balance of the farming pool. If there are not enough tokens on the balance to pay all the rewards, the pool will be automatically marked with a danger icon in the general list.

![](<../../../.gitbook/assets/image (9).png>)

### Changing the farming speed

The administrator can increase or decrease the farming speed. To do that, one needs to indicate the start of a new farming period and a new farming speed.

![](<../../../.gitbook/assets/image (200).png>)

### Closing the pool

The administrator can at any time specify the date when the farming pool closes. At this point, the last unit of the reward will be distributed.

Attention! You can only set the closing date once. After establishing an end date, you can neither change the date nor add another farming period.

![](<../../../.gitbook/assets/image (50).png>)

### Withdrawal of unclaimed tokens

If the administrator has deposited more reward tokens than necessary, these tokens can be withdrawn. To do so, you need to set the end date for farming, and then wait for the end of vesting + lockdown period (30 days).

![](<../../../.gitbook/assets/image (53).png>)
