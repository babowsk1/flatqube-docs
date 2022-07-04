---
description: With this smart contract you can swap evers to Tip3 tokens.
---

# EverToTip3

Smart contract responsible for swapping evers to Tip3 tokens.

Derives following classes and interfaces: *IAcceptTokensMintCallback, IAcceptTokensTransferCallback, IAcceptTokensBurnCallback, IEverTip3SwapEvents*.

### **`constructor`** 

```
constructor() public
```

Deploys wallet with `EverToTip3` contract address.

### **`buildExchangePayload`** 

```
function buildExchangePayload(uint64 id, uint128 amount, address pair, uint128 expectedAmount, uint128 deployWalletValue) external pure returns (TvmCell)
```

Creates payload constructor for swap between Ever and Tip-3 token - takes id, amount, pair address, expectedAmount, `deployWalletValue` from params and store those values to the `TVMBuilder` instance.  

**Parameters:**

| Name              | Type    | Description                    |
|-------------------|---------|--------------------------------|
| id                | uint64  | Payload Id                     |
| amount            | uint128 | Amount to exchange             |
| pair              | address | Exchange pair root address     |
| expectedAmount    | uint128 | Expected amount after exchange |
| deployWalletValue | uint128 | Value for deploying new wallet |

**Return Value:**

| Type    | Description                     |
|---------|---------------------------------|
| TvmCell | Exchange payload in cell format |

## Swap

### **`swapEvers`** 

```
function swapEvers(address user, TvmCell payload) external
```

Takes user address and payload as params if there are enough EVERs swap them with Tip-3 token, if not cancel.
	
**Parameters:**

| Name    | Type    | Description                             |
|---------|---------|-----------------------------------------|
| user    | address | Address of the user initiating exchange |
| payload | TvmCell | Payload used for wrapping EVERs         |

## Callbacks

### **`onWeverWallet`** 

```
function onWeverWallet(address _weverWallet) external
```

Deploys Wever wallet for the contract using `_weverWallet` address from the function params.


**Parameters:**

| Name         | Type    | Description                             |
|--------------|---------|-----------------------------------------|
| _weverWallet | address | Address used to initialize wever wallet |

### **`onAcceptTokensMint`** 

```
function onAcceptTokensMint(address /*tokenRoot*/, uint128 amount, address user, TvmCell payload) override external
```

Checks if weverWallet is the message sender and message sender value is greater than 0, if value is ge then `SWAP_EVER_TO_TIP_3_MIN_VALUE`, if so emit `SwapEverToTip3WeverMint` event, create success, cancel and result payload, transfer the amount from the function params of tokens from `EverToTip3` wallet to the pair’s address, else transfer to the `weverVault` address (burn Wevers).


**Parameters:**

| Name       | Type    | Description                                                                  |
|------------|---------|------------------------------------------------------------------------------|
| token_root | address | Address of the token root                                                    |
| amount     | uint128 | Amount of tokens to transfer to user                                         |
| user       | address | Address of the user to transfer remaining gas                                |
| payload    | TvmCell | Payload with exchange data (id, amount, pair, expectedAmount, deploy value…) |

### **`onAcceptTokensTransfer`** 

```
function onAcceptTokensTransfer(address /*tokenRoot*/, uint128 amount, address sender, address /*senderWallet*/, address user, TvmCell payload) override external
```

If operationStatus is cancel, burn WEVERs (transfer them to `weverVault` address), if it is SUCCESS call the callback function for swapping evers to tip 3 (`onSwapEversToTip3Success`), emit `SwapEversToTip3SuccessTransfer` event and send tip 3 tokens to the user using `TokenWallet`’s transfer function.     
If it’s not SUCCESS or CANCEL set `needCancel` var to true and transfer the amount back to the sender.


**Parameters:**

| Name         | Type    | Description                               |
|--------------|---------|-------------------------------------------|
| tokenRoot    | address | Address of token root                     |
| amount       | uint128 | Amount of tokens to transfer              |
| sender       | address | Address of tokens sender                  |
| senderWallet | address | Tokens sender’s wallet address            |
| user         | address | User’s address for receiving tip3 tokens  |
| payload      | TvmCell | Transfer payload data                     |

### **`onAcceptTokensBurn`** 

```
function onAcceptTokensBurn(uint128 /*amount*/, address /*walletOwner*/, address /*wallet*/, address user, TvmCell payload) override external
```

Callback function used when swap is canceled. Emit `SwapEverToTip3CancelTransfer` and call callback function `onSwapEverToTip3CancelTransfer`.
	
**Parameters:**

| Name        | Type    | Description                            |
|-------------|---------|----------------------------------------|
| amount      | uint128 | Amount of tokens to burn (optional)    |
| walletOwner | address | Address of wallet owner                |
| wallet      | address | Wallet address                         |
| user        | address | User’s address that canceled exchange  |
| payload     | TvmCell | Burn tokens payload data               |

## Key Events

### **`SwapEverToTip3WeverMint`**

```
SwapEverToTip3WeverMint(uint64 id, uint128 amount, address pair, uint128 expectedAmount, uint128 deployWalletValue);
```

Emitted inside `onAcceptTokensMint` callback.

### **`SwapEverToTip3SuccessTransfer`**

```
SwapEverToTip3SuccessTransfer(address user, uint64 id);
```

Emitted inside `onAcceptTokensTransfer` callback when EVERs are successfully swapped to Tip3 tokens.

### **`SwapEverToTip3CancelTransfer`**

```
SwapEverToTip3CancelTransfer(address user, uint64 id);
```

Emitted inside of the onAcceptTokensBurn when swap is canceled .
