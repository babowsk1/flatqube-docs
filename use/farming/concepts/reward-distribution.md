# Reward distribution

Reward tokens are those issued to stakeholders who have locked their funds in the farming pool.

The main indicator of reward distribution is farming speed.

The farming speed is the number of tokens evenly distributed among all stakeholders per second.

Every second, a part of your reward gets into the Locked reward section. \
Afterwards, the rewards are unlocked with the help of [vesting](vesting.md).

In [old farming pools](../old-farming/), the speed is set manually by the [pool administrator](../old-farming/interface/farm-page-administrator.md) - it is needed just to enter the amount of tokens that will be distributed every second.

However, in [new farming pools](../new-farming/) (gauges), this process is quite different.

You can still manually add reward tokens (not QUBEs) and set a certain speed of their distribution. However, the main reward token in the new farming pools is QUBE. \
Manually adding it as a reward is no longer impossible.

Determination of the number of QUBE rewards is accomplished by the [FlatQube DAO](../../dao/).

Every Epoch (two weeks) there is a vote for the distribution of all QUBEs in proportion to the votes cast for a certain farming pool (virtual veQUBE tokens).

Within the next two weeks after the end of the voting, all QUBEs allocated to the farming pool will be evenly distributed among all stakeholders.

Example:

As a result of voting in Epoch No. 2, 8,105 veQUBEs were cast as votes for the USDT/USDC farming pool, which is 11.09% of all votes cast in this Epoch.\
In this Epoch, the number of distributed QUBEs is 42350.

Accordingly, from the end of voting in this Epoch until the end of voting in the next one, 11.09% of 42350 QUBEs, which is equal to 4694 QUBE, will be distributed in the USDT/USDC farming pool. The speed of farming in this case is 0.00388139 QUBEs per second.
