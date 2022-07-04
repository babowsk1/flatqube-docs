---
discription: The EverWeverToTip3 defines the logic for swapping EVERs in combination with WEVERs to Tip3 tokens.
---

# EverWeverToTip3

Smart contract responsible for swapping EVERs in combination with WEVERs to Tip3 tokens.

Derives following classes and interfaces: *IAcceptTokensTransferCallback, IAcceptTokensBurnCallback*.

### **`constructor`** 

```
constructor() public
```

Deploy EverToTip3Gas empty wallet.

### **`buildExchangePayload`** 

```
function buildExchangePayload(uint64 id, uint128 amount, address pair, uint128 expectedAmount, uint128 deployWalletValue) external pure returns (TvmCell)
```

Builds payload by filling the TVM builder instance with data derived from function params, returns builder converted to cell.

**Parameters:**

| Name              | Type    | Description                              |
|-------------------|---------|------------------------------------------|
| id                | uint64  | Operation id                             |
| amount            | uint128 | Amount of tokens to exchange             |
| pair              | address | Address of the exchange pair             |
| expectedAmount    | uint128 | Expected amount of tokens after exchange |
| deployWalletValue | uint128 | Deploy value                             |

**Return Value:**

| Type    | Description                     |
|---------|---------------------------------|
| TvmCell | Exchange payload in cell format |

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

### **`onAcceptTokensTransfer`** 

```
function onAcceptTokensTransfer(address /*tokenRoot*/, uint128 amount, address /*sender*/, address /*senderWallet*/, address user, TvmCell payload) override external
```

Callback if swap between ever and tip 3 is successful.  
Calls `onSwapEverToTip3Success` callback to the user, `SwapEverToTip3SuccessTransfer` event is emitted and tip 3 tokens are sent to a user wallet by calling `TokenWallet`’s transfer method.  
If conditions are not fulfilled swap is canceled and tokens are returned to sender’s wallet.

**Parameters:**

| Name         | Type    | Description                               |
|--------------|---------|-------------------------------------------|
| tokenRoot    | address | Address of token root (optional)          |
| amount       | uint128 | Amount of tokens to transfer              |
| sender       | address | Address of tokens sender (optional)       |
| senderWallet | address | Tokens sender’s wallet address (optional) |
| user         | address | User’s address for receiving tip3 tokens  |
| payload      | TvmCell | Transfer payload data                     |

### **`onAcceptTokensBurn`** 

```
function onAcceptTokensBurn( uint128 /*amount*/, address /*walletOwner*/, address /*wallet*/, address user, TvmCell payload) override external
```

If result of swap was canceled call this callback, it emits `SwapEverToTip3CancelTransfer` event and calls `onSwapEversToTip3Cancel` callback.

**Parameters:**

| Name        | Type    | Description                            |
|-------------|---------|----------------------------------------|
| amount      | uint128 | Amount of tokens to burn (optional)    |
| walletOwner | address | Address of wallet owner (optional)     |
| wallet      | address | Wallet address (optional)              |
| user        | address | User’s address that canceled exchange  |
| payload     | TvmCell | Burn tokens payload data               |

## Key Events

### **`SwapEverWeverToTip3Unwrap`**

```
SwapEverWeverToTip3Unwrap(address user, uint64 id);
```