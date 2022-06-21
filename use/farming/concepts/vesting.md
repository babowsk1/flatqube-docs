# Vesting

## Vesting <a href="#f5e5" id="f5e5"></a>

As previously mentioned, rewards for farming are accrued constantly, but they do not immediately become available for withdrawal. The distribution of rewards on [**FlatQube**](https://flatqube.io) is done in accordance with a **Vesting** mechanism.

**Vesting** is a market oversupply management tool that was created as a result of increased TVL and farming speed. The essence of vesting is to reduce the pressure on the price of tokens and encourage more long-term investors.

Essentially, vesting on [**FlatQube**](https://flatqube.io) is a formula for progressively unlocking a liquidity provider’s rewards over time.

Each farming pool has several parameters related directly to vesting (the values ​​of these parameters can be found on the page of each pool):\
**Vesting Ratio, Vesting Period, Vesting end date.**

And the rewards themselves are indicated as **Unclaimed reward** and **Entitled reward**.

We are going to break down what each of these terms means.

**Vesting ratio** is the percentage of the reward that will be sent to vesting, and **Vesting period** is the time frame during which vesting will take place.

**Vesting end date** is the date at which all rewards that have accumulated in vesting will be unlocked.

**Entitled reward** is a parameter that shows the number of tokens that are in vesting and not available for withdrawal (Claim) at the moment. These tokens are gradually unlocked, and when they become available to withdraw they will be shown in the **Unclaimed reward** column.

The accumulation of **Unclaimed rewards** from the amount locked in vesting (**Entitled reward**), begins immediately once they are received and ends once the **Vesting period** has expired.

For example, if the **Vesting ratio** is 100% and the **Vesting period** is 120 days, it means that 50% of all tokens received as rewards will be sent to the user over the course of 110 days (these tokens will be displayed in the **Unclaimed reward** section). The remaining tokens will be sent over the course of the next 130 days.

The rewards that are not yet available and that will be unlocked over the course of 120 days will be displayed in the **Entitled reward** section. Below we are going to take a look at how this works.

In layman’s terms, every day 1/120th of the rewards that have accumulated in Entitled reward are sent to Unclaimed reward. Accordingly, every second 1/(60\*60\*24\*120) of the **Entitled reward** is unlocked.

It is important to note that the share of unlocked funds is calculated from the current Entitled reward balance while your liquidity is locked in the farming pool, but once you decide to withdraw your LP tokens, the remaining Entitled reward balance will be unlocked in even shares every second. Put simply, the balance of the **Entitled reward** will be transferred to the **Unclaimed reward** in equal shares within 120 days from the moment the LP tokens are withdrawn from the farming pool.

We highlight that the **Vesting end date** will constantly change until you withdraw your liquidity from a farming pool.\
This happens because rewards are received every second and instantly blocked and then sent to vesting in the form of **Entitled rewards** for future unlocking evenly over the next 120 days.

When LP tokens are withdrawn from a farming pool, the **Entitled reward** will continue to be unblocked and sent to your **Unclaimed reward** over the course of 120 days and the number of your **Entitled Reward** will not increase.

Example 1: you have LP tokens in farming and you receive 1 wEVER every second. Your total reward after the first second is 1 wEVER, after the 2nd second is 2 wEVER, after the 3rd second is 3 wEVER, and so on.

Accordingly, your **Unclaimed reward**, which gets unlocked progressively, after the 2nd second is equal to the following:

![(1) after the 2nd second](https://miro.medium.com/max/394/0\*nvkSZbnX8UQGpz7G)

![(2) after the 3rd second](https://miro.medium.com/max/362/0\*dkVWQ5aWeWAVLUVB)

![(3) after the 4th second](https://miro.medium.com/max/392/0\*C4yDdi8gRQm0OlUF)

and the total **Unclaimed reward**, after the 4th second is equal to (1) + (2) + (3)

Example 2:

Let’s stay you have withdrawn your tokens from a farming pool and at that moment you had an **Entitled reward** of 10 wEVER. From the moment you withdrew your funds, your **Entitled reward** will no longer increase. This means that every second you will receive 10/(60\*60\*24\*120) wEVER and you will receive the remaining reward over the course of 120 days.

Here is a graph to illustrate:

![](https://miro.medium.com/max/1400/0\*PFBNKSshe6ypwe5f)

Vesting graph displaying a **Vesting ratio** of 100% and a **Vesting period** of 120 days

This is a vesting graph with a **Vesting ratio** of 100% and a **Vesting period** of 120 days. The graph displays a **Vesting Period** of 120 days — after 120 days, your LP tokens are withdrawn, and the **Entitled reward** earned during this time continues to be unlocked and transferred to the **Unclaimed reward**.

At all times we have the following 2 parameters:

1\. **Entitled reward** — total of locked rewards

2\. **Unclaimed reward** — total of unlocked rewards

To calculate the Unclaimed we have a few additional parameters:

* now (the current time)
* lCT — lastClaimTime (time of the last claim)
* vP- vestingPeriod
* pVI — partlyVestedInterval (partial vesting period)
* fVI — fullVestedInterval (entire vesting period)

Depending on how much time has passed since the last **Claim**, there are 2 scenarios for when more or less than the vesting period has passed.

If less has passed, the calculations must be made according to F1.

If more has passed, you need to calculate the required value using the F2 system. In fact, all you have to do is simply cut off part of the amount that was completely unlocked, and for the remaining, use the function from F1.

![](https://miro.medium.com/max/1344/0\*H2hu9nxnyjBiJYI0)

\\
