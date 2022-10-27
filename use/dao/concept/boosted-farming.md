# Boosted farming

## What’s this?

Boosted farming is a virtual increase in your balance. In other words, this virtual increase in the balance increases the farming speed.

Your virtual balance can be increased through either locked QUBE (veQUBE) or locked LP tokens sent for farming. When you create a pool in the new farm, boosted farming from veQUBE takes place automatically, while the boost from locking LP is configured when you add a pool to the new farm and can range from zero to four years.

## Increasing your balance through veQUBE:

Total deposits (TD) — is just the total amount of the user’s deposits in a specific gauge. We need this new entity when measuring locked deposits.

![](<../../../.gitbook/assets/image (12).png>)

Where:

* **d** — user’s deposit.
* **n** — number of deposits.

veQUBE — vote escrowed tokens, which can be obtained by locking QUBE.\
The amount of veQUBE remains static for the whole duration of the lock.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Were:

* **QUBE lock time** – lock time in days.

Ve-boosted deposit (veBD) – part of the virtual balance which is calculated from the user’s veQUBE amount:

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Where:

* **GB** – gauge balance, sum of user balances in a specific gauge (e.g. EVER/USDT).
* **veQUBE** – number of veQUBE that the user has.
* **TveQUBE** – total circulating supply of veQUBE.

## Increasing your balance through locking LP

LP-locked boosted deposit (BD) – part of the virtual balance which is calculated from the time the deposit is locked.

![](<../../../.gitbook/assets/image (27).png>)

Where:

* **Deposit lock time** – the time that the user has blocked their LP tokens for.
* **Max. lock time** – maximum possible LP lock time.
* **d** – user deposit.

## Summation of boosts from veQube and LP

Ve-boosted deposit multiplier (veBD multiplier) – boost we get for veQUBE\
![](<../../../.gitbook/assets/image (29).png>)

LP-locked boosted deposit multiplier (lBD multiplier) – boost we get for locked LP

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Finally, virtual balance — the balance to which the user’s weight in the farming pool will be applied

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### **Conclusion**

Farming is credited to the user’s virtual balance, so anyone who does not have a locked deposit or locked QUBE will get less rewards than previously. The average farming speed is almost unchanged, but the (virtual) balance to which the reward will be credited will increase; therefore, the real balance that was there before will give less.

## Examples

User A $1 \
10 veQUBE;\
\
user B $1,000 \
10,000 veQUBE;\
\
EVER/USDT \
TVL – $10,000; \
veQUBE supply – 100,000

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

**User A pool weight:**

_**before**_ 1/10,000 = 0.01%

_**after**_ 2.5/11,501.5 = 0.02174%

**User B pool weight:**

_**before**_ 1,000/10,000 = 10%

_**after**_ 2,500/11,501.5 = 21.74%

**Other users pool weight:**

_**before**_ 8,999/10,000 = 89.99%

_**after**_ 8,999/11,501.5 = 78.24%
