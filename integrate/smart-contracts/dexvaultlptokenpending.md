---
description: This smart contract is used for creating and deploying dex vault’s liquidity pool token and it’s wallets so it can change its state from pending.
---

# DexVaultLpTokenPending

Smart contract responsible for creating and deploying dex vault’s liquidity pool token and it’s wallets so it can change its state from pending.

Derives following classes and interfaces:   *ITokenRootDeployedCallback, ITransferTokenRootOwnershipCallbac*

### **`Constructor`** 

```
constructor(address token_factory_, uint128 value_, address send_gas_to_) public onlyVault
```

Based on parameters such as token factory address, deploy value and `send_gas_to` address fills the right and left root symbol data and deploys pending dex vault’s liquidity pool token smart contract.

**Parameters:**

| Name          | Type    | Description                                                 |
|---------------|---------|-------------------------------------------------------------|
| token_factory | address | Token factory address used for deploying lp tokens          |
| value         | uint128 | Deploy value                                                |
| send_gas_to   | address | Address where to send gas spent by calling contract methods |

### **`terminate`** 

```
function terminate() public view
```

Terminates deploy of the pending liquidity pool token and calls _onLiquidityTokenNotDeployed function

## Callbacks

### **`onSymbol`** 

```
function onSymbol(string symbol) public onlyExpectedToken
```

Receives token symbol as a parameter, decrements pending messages and whether the sender is right or left root fills the root data with received symbol value and calls createLpTokenAndWallets.  
If the sender is not right/left root calls `terminateIfEmptyQueue`.

**Parameters:**

| Name   | Type   | Description                                 |
|--------|--------|---------------------------------------------|
| symbol | string | Token symbol used for creating new lp token |

### **`onTokenRootDeployed`** 

```
function onTokenRootDeployed(uint32 /*answer_id*/, address token_root) override public onlyTokenFactory
```

Receives answerId and token root address through parameters, fills liquidity pool token root with token root value, deploys empty wallet using the token root and vault address, fills the callback params and transfers ownership to the new liquidity pair address calling the transferOwnership function from the `TransferableOwnership` contract.

**Parameters:**

| Name       | Type    | Description                                                   |
|------------|---------|---------------------------------------------------------------|
| answer_id  | uint32  |                                                               |
| token_root | address | Token root address of the lp token, used for deploying wallet |

### **`onTransferTokenRootOwnership`** 

```
function onTransferTokenRootOwnership( address oldOwner, address newOwner, address, TvmCell) external override
```

Gets old owner address and new owner address through parameters and if the old owner is address of the `DexVaultLpTokenPending` smart contract and the new owner is dex pair address then token root ownership is delegated to the new owner address and deployed token root data (token root wallets, reserved initial balance, pair data configured…) is configured by calling DexVault’s `onLiquidityTokenDeployed` if not calls `onLiquidityTokenNotDeployed`.

**Parameters:**

| Name     | Type    | Description                             |
|----------|---------|-----------------------------------------|
| oldOwner | address | Address of the old token root’s owner   |
| newOwner | address | Address of the new owner                |
| -        | address | Address used for checking the ownership |
| -        | TvmCell |                                         |

## Lp token and wallet

### **`createLpTokenAndWallets`**

```
function createLpTokenAndWallets() private
```

Calling `lpTokenSymbol` gets the name of the symbol based on the right and left root symbol, deploys lp token calling `deployLpToken`, deploys wallets for left and right root and their vaults by calling `deployEmptyWallet` function.

### **`deployLpToken`**

```
function deployLpToken(bytes symbol, uint8 decimals) private
```

Takes symbol and number of decimals and deploys token calling createToken function of the `TokenFactory` based on the function (`deployLpToken`) parameters.

**Parameters:**

| Name        | Type    | Description                                                 |
|-------------|---------|-------------------------------------------------------------|
| pair        | address | Pair address                                                |
| left_root   | address | Token root address of the left token                        |
| right_root  | address | Token root address of the right token                       |
| send_gas_to | address | Address where to send gas spent by calling contract methods |

### **`deployEmptyWallet`** 

```
function deployEmptyWallet(address token_root, address wallet_owner) private
```

Takes `token_root` and `wallet_owner` addresses as parameters and based on those addresses deploys wallet calling TokenRoot’s `deployWallet` function.

**Parameters:**

| Name         | Type    | Description                                       |
|--------------|---------|---------------------------------------------------|
| token_root   | address | Token root address used for deploying new wallet  |
| wallet_owner | address | Wallet owner address                              |

### **`lpTokenSymbol`** 

```
function lpTokenSymbol(string left_symbol, string right_symbol) private view returns (string)
```

Creates liquidity pool token symbol based on the name of the left and right roots’ symbols and returns name of the lp token symbol.
	
**Parameters:**

| Name         | Type   | Description             |
|--------------|--------|-------------------------|
| left_symbol  | string | Left pair token symbol  |
| right_symbol | string | Right pair token symbol |

**Return Value:**

| Type   | Description                 |
|--------|-----------------------------|
| string | Liquidity pool token symbol |

