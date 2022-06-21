# Tokens we use

## Token standard

FlatQube uses a common standard for Everscale network tokens - TIP-3.1. The need to use TIP-3.1 tokens is due to the technical features of the Everscale blockchain, aimed at reducing transaction fees, increasing reliability and speed through dynamic sharding and P2P architecture. See TIP-3.1 for details. Here are some useful links:

{% embed url="https://everscale-org.github.io/Standard/TIP-3/core-description" %}

{% embed url="https://broxus.medium.com/tip-3-1-token-guide-a13169ff6017" %}

## Root contract

The token root contract stores general information about the token, e.g. name, symbol, decimals, token wallet code and so on.

## User contract

Each token holder has its own instance of a token wallet contract. Transfers happen in a decentralized fashion - a sender token wallet SHOULD send a specific message to a receiver token wallet. Since token wallets have the same code, it's easy for receiver token wallets to check the correctness of sender token wallets.

\\
