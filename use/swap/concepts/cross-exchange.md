# Cross-exchange

As you know, the ability to exchange one token for another on FlatQube is provided by the [liquidity in pools](../../pools/).\
In the event that there is not enough liquidity in the corresponding pool, or the required pool does not exist at all, **Cross-exchange** will help you.\
The essence of Cross-exchange is to interact with several liquidity pools at once:\
Let's say you need to exchange token A for token B, but the corresponding pool does not exist. In this case, FlatQube will suggest performing a cross-exchange swap, in which token A will be exchanged for token C (interacting with the A/C pool), and then token C will be exchanged for token B (interacting with the C/B pool).

You should bear in mind that since you are interacting with two pools at once, your [**slippage tolerance**](slippage-tolerance.md), as well as [**Liquidity providers fee**](fees.md), doubles.

{% content-ref url="../how-to/use-cross-exchange.md" %}
[use-cross-exchange.md](../how-to/use-cross-exchange.md)
{% endcontent-ref %}
