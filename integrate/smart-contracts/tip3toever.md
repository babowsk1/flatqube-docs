---
description: The Tip3ToEver smart contract defines the logic for swapping Tip3 To Ever.
---

# Tip3ToEver

Smart contract responsible for swapping Tip3 token to Ever.

Derives following classes and interfaces: *IAcceptTokensTransferCallback, IAcceptTokensBurnCallback, IEverTip3SwapEvents*.

### **`constructor`** 

```
constructor() public
```

Deploy empty wallet.

### **`buildExchangePayload`** 

```
function buildExchangePayload(uint64 id, address pair, uint128 expectedAmount) external pure returns (TvmCell)
```

Build payload constructor for exchanging TIP 3 to EVER, store values from function params to `TVMBuilder` instance.

Parameters:

| Name           | Type    | Description                              |
|----------------|---------|------------------------------------------|
| id             | uint64  | Id of the operation call                 |
| pair           | address | Address of the exchange pair             |
| expectedAmount | uint128 | Expected amount of tokens after exchange |

## Callbacks

### **`onWeverWallet`** 

```
function onWeverWallet(address _weverWallet) external
```

Callback deploy for `weverWallet`.

Parameters:

| Name         | Type    | Description                 |
|--------------|---------|-----------------------------|
| _weverWallet | address | Address of the WEVER wallet |

### **`onAcceptTokensTransfer`** 

```
function onAcceptTokensTransfer(address /*tokenRoot*/, uint128 amount, address sender, address /*senderWallet*/, address user,TvmCell payload) override external
```

Callback for swap. If operationStatus is SWAP and value is greater than `SWAP_TIP3_TO_EVER_MIN_VALUE`, build success, cancel and `resultPayload` and transfer from `Tip3ToEver` wallet to the pair’s wallet.    
If operationStatus is CANCEL emit `SwapTip3EverCancelTransfer` event and call `OnSwapTip3ToEverCancel` callback and transfer the amount back to the user, if SUCCESS and msg sender is `weverWallet`, transfer the amount to weverVault wallet.    
Else if needCancel var is true transfer value back to the sender

Parameters:

| Name         | Type     | Description                               |
|--------------|----------|-------------------------------------------|
| tokenRoot    | address  | Address of token root                     |
| amount       | uint128  | Amount of tokens to transfer              |
| sender       | address  | Address of tokens sender                  |
| senderWallet | address  | Tokens sender’s wallet address            |
| user         | address  | User’s address for receiving EVER tokens  |
| payload      | TvmCell  | Transfer payload data                     |

### **`onAcceptTokensBurn`** 

```
function onAcceptTokensBurn(uint128 /*amount*/, address /*walletOwner*/, address /*wallet*/, address user, TvmCell payload) override external
```

Callback for burn if the swap succeeded, emits `SwapTip3EverSuccessTransfer` event and call callback `onSwapTip3ToEverSuccess`.

Parameters:

| Name        | Type     | Description                            |
|-------------|----------|----------------------------------------|
| amount      | uint128  | Amount of tokens to burn (optional)    |
| walletOwner | address  | Address of wallet owner                |
| wallet      | address  | Wallet address                         |
| user        | address  | User’s address that canceled exchange  |
| payload     | TvmCell  | Burn tokens payload data               |

## Key Events

### **`SwapTip3EverSuccessTransfer`**

```
SwapTip3EverSuccessTransfer(address user, uint64 id);
```

Emitted inside `onAcceptTokensTransfer` callback when Tip3 tokens are successfully swapped to EVERs.

### **`SwapTip3EverCancelTransfer`**

```
SwapTip3EverCancelTransfer(address user, uint64 id);
```

Emitted inside `onAcceptTokensTransfer` callback when swap is canceled.

