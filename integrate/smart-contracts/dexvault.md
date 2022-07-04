---
description: The DexVault smart contract is used for creating vault and filling initial data.
---

# DexVault

Smart contract responsible for creating vault and filling initial data such as lp token, platform code, owner and manipulating vault’s transactions (transfer, withdraw).

Derives following classes and interfaces:   
<u> *DexContractBase, IDexVault, IUpgradable, IResetGas.* </u>

### **`constructor`** 

```
constructor (address owner_, address root_, address token_factory_) public
```

Sets gas limit to maximum (`tvm.accept`) and sets values for root, owner and token factory address.

**Parameters:**

| Name           | Type     | Description                    |
|----------------|----------|--------------------------------|
| owner_         | address  | Address of the dex vault owner |
| root_          | address  | Address of the dex vault root  |
| token_factory_ | address  | Address of the token factory   |

### **`_dexRoot`** 

```
function _dexRoot() override internal view returns(address)
```

Returns the root address of the DexVault.

**Return value:**

| Type    | Description             |
|---------|-------------------------|
| address | Address of the dex root |

### Owner

### **`transferOwner`** 

```
function transferOwner(address new_owner) public override onlyOwner
```

Pending owner address gets value of the new owner param which is used in acceptOwner method (where actual transfer of ownership is happening) and emits `RequestedOwnerTransfer` event.

**Parameters:**

| Name      | Type    | Description                    |
|-----------|---------|--------------------------------|
| new_owner | address | Address of the new vault owner |

### **`acceptOwner`** 

```
function acceptOwner() public override
```

Accepts new owner in a way that owner becomes pending owner and emits `OwnerTransferAccepted` event.

### **`getOwner`** 

```
function getOwner() external view responsible returns (address)
```

Returns DexVault owner address.

**Return value:**

| Type    | Description |
|---------|-------------|
| address |             |

### **`getPendingOwner`** 

```
function getPendingOwner() external view responsible returns (address)
```

Returns DexVault’s pending owner address.

**Return value:**

| Type    | Description                                   |
|---------|-----------------------------------------------|
| address | Address of the pending owner of the dex vault |

### Token

### **`setTokenFactory`** 

```
function setTokenFactory(address new_token_factory) public override onlyOwner
```

Sets new address of token factory by passing new address from function params to token factory contract param, emits TokenFactoryAddressUpdated event with previous token factory address and a new one.

**Parameters:**

| Name              | Type    | Description                      |
|-------------------|---------|----------------------------------|
| new_token_factory | address | Address of the new token factory |

### **`installPlatformOnce`** 

```
function installPlatformOnce(TvmCell code) external onlyOwner
```

Checks whether the platform is already installed, if not, reserves initial balance, passes code value to the platform code and transfers gas.

**Parameters:**

| Name | Type    | Description                       |
|------|---------|-----------------------------------|
| code | TvmCell | Platform code for initial version |

### **`installOrUpdateLpTokenPendingCode`** 

```
function installOrUpdateLpTokenPendingCode(TvmCell code) public onlyOwner
```

Reserves initial balance, passes new code to lp token pending code.

**Parameters:**

| Name | Type    | Description                 |
|------|---------|-----------------------------|
| code | TvmCell | Liquidity pool pending code |

### **`addLiquidityToken`** 

```
function addLiquidityToken(address pair, address left_root, address right_root, address send_gas_to) public override onlyPair(left_root, right_root)
```

Creates new instance of `DexVaultLpTokenPending`, pass necessary params such as token factory address, value and address for receiving gas.

**Parameters:**

| Name        | Type    | Description                                                 |
|-------------|---------|-------------------------------------------------------------|
| pair        | address | Pair address                                                |
| left_root   | address | Token root address of the left token                        |
| right_root  | address | Token root address of the right token                       |
| send_gas_to | address | Address where to send gas spent by calling contract methods |

### **`onLiquidityTokenDeployed`** 

```
function onLiquidityTokenDeployed(uint32 nonce, address pair, address left_root, address right_root, address lp_root, address send_gas_to) public override onlyLpTokenPending(nonce, pair, left_root, right_root)
```

Callback function, builds initial token pending data based on the params passed by `onlyLpTokenPending`, reserves initial balance calls the `liquidityTokenRootDeployed` method from the DexPair where the token root wallets are configured and the new pair is created.

**Parameters:**

| Name        | Type    | Description                                                 |
|-------------|---------|-------------------------------------------------------------|
| nonce       | uint32  | Flag used in building initial state of tvm                  |
| pair        | address | Address of the liquidity pool                               |
| left_root   | address | Token root address of the left token                        |
| right_root  | address | Token root address of the right token                       |
| lp_root     | address | Liquidity pool root address                                 |
| send_gas_to | address | Address where to send gas spent by calling contract methods |

### **`onLiquidityTokenNotDeployed`** 

```
function onLiquidityTokenNotDeployed( uint32 nonce, address pair, address left_root, address right_root, address lp_root, address send_gas_to) public override onlyLpTokenPending(nonce, pair, left_root, right_root)
```

Callback function, builds initial token pending data based on the params passed by `onlyLpTokenPending`, calls the `liquidityTokenRootNotDeployed` method from the DexPair where it does the transfer from `send_gas_to` address based on active variable.

**Parameters:**

| Name        | Type    | Description                                                 |
|-------------|---------|-------------------------------------------------------------|
| nonce       | uint32  | Flag used in building initial state of tvm                  |
| pair        | address | Address of the liquidity pool                               |
| left_root   | address | Token root address of the left token                        |
| right_root  | address | Token root address of the right token                       |
| lp_root     | address | Liquidity pool root address                                 |
| send_gas_to | address | Address where to send gas spent by calling contract methods |

### **`_buildLpTokenPendingInitData`** 

```
function _buildLpTokenPendingInitData(uint32 nonce, address pair, address left_root, address right_root) private view returns (TvmCell)
```

Builds pending liquidity pool token initial data calling tvm’s buildStateInit method where it returns TvmCell with initialized state using `DexVaultLpTokenPending` contract, additional data for the contract such as nonce, vault, pair, left, right address and `lp_token_pending_code` as required code param for buildStateInit method

**Parameters:**

| Name       | Type    | Description                                |
|------------|---------|--------------------------------------------|
| nonce      | uint32  | Flag used in building initial state of tvm |
| pair       | address | Address of the liquidity pool              |
| left_root  | address | Token root address of the left token       |
| right_root | address | Token root address of the right token      |

**Return value:**

| Type    | Description                          |
|---------|--------------------------------------|
| TvmCell | Data used for building initial state |

## Withdraw

### **`withdraw`** 

```
function withdraw( uint64 call_id, uint128 amount, address /* token_root */, address vault_wallet, address recipient_address, uint128 deploy_wallet_grams, address account_owner, uint32 /* account_version */, address send_gas_to ) external override onlyAccount(account_owner)
```

Used for withdraw transaction, called from dex pair, transfers tokens from vault token wallet to recipient address through the transfer method from TokenWallet.    
Emits `WithdrawToken` event and calls `successCallback` to notify success.

**Parameters:**

| Name        | Type    | Description                                                 |
|-------------|---------|-------------------------------------------------------------|
| nonce       | uint32  | Flag used in building initial state of tvm                  |
| pair        | address | Address of the liquidity pool                               |
| left_root   | address | Token root address of the left token                        |
| right_root  | address | Token root address of the right token                       |
| lp_root     | address | Liquidity pool root address                                 |
| send_gas_to | address | Address where to send gas spent by calling contract methods |

## Transfer

### **`transfer`** 

```
function transfer(uint128 amount, address /* token_root */, address vault_wallet, address recipient_address, uint128 deploy_wallet_grams, bool    notify_receiver, TvmCell payload, address left_root, address right_root, uint32  /* pair_version */, address send_gas_to ) external override onlyPair(left_root, right_root)
```

Does the pair transfer tokens through the transfer method of the TokenWallet from vault wallet to the recipient’s address, emits `PairTransferTokens` event.

**Parameters:**

| Name                | Type     | Description                                                     |
|---------------------|----------|-----------------------------------------------------------------|
| amount              | uint128  | Amount to be transferred                                        |
| token_root          | address  | Address of the token root which will be transferred             |
| vault_wallet        | address  | Address of vault’s wallet                                       |
| recipient_address   | address  | Address of the recipient of the transaction                     |
| deploy_wallet_grams | uint128  | Fee for deploying wallet                                        |
| notify_receiver     | bool     | Indicates if the receiver of the transaction should be notified |
| payload             | TvmCell  | Additional data needed for transfering to token wallet          |
| left_root           | address  | Token root address of the left token                            |
| right_root          | address  | Token root address of the right token                           |
| pair_version        | uint32   | Current pair version                                            |
| send_gas_to         | address  | Address where to send gas spent by calling contract methods     |

## Code upgrade

### **`upgrade`** 

function upgrade(TvmCell code) public override onlyOwner

Reserves initial balance, makes new builder instance to store all the vault’s data necessary, set passed code for upgrade and finishes upgrade of DexVault by calling onCodeUpgrade

**Return value:**

| Name | Type    | Description                         |
|------|---------|-------------------------------------|
| code | TvmCell | Code to be set for upgraded version |

## Reset

### **`resetGas`** 

```
function resetGas(address receiver) override external view onlyOwner
```

Resets balance to `ROOT_INITIAL_BALANCE`.

**Return value:**

| Name     | Type    | Description                                                 |
|----------|---------|-------------------------------------------------------------|
| receiver | address | Address where to send gas spent by calling contract methods |

### **`resetTargetGas`** 

```
function resetTargetGas(address target, address receiver) external view onlyOwner
```

Calculates max between `ROOT_INITIAL_BALANCE` and after that resets gas to calculated value for target address calling 
`resetGas` method.

**Return value:**

| Name     | Type    | Description                                                 |
|----------|---------|-------------------------------------------------------------|
| target   | address | Address for which gas should be reset                       |
| receiver | address | Address where to send gas spent by calling contract methods |

## Key Events

### **`VaultCodeUpgraded`**

```
VaultCodeUpgraded();
```

Emitted when vault code is upgraded

### **`RequestedOwnerTransfer`**

```
RequestedOwnerTransfer(address old_owner, address new_owner);
```

Emitted when ownership transfer is requested.

### **`OwnerTransferAccepted`**

```
OwnerTransferAccepted(address old_owner, address new_owner);
```

Emitted when ownership transfer is accepted.

### **`TokenFactoryAddressUpdated`**

```
TokenFactoryAddressUpdated(address old_token_factory, address new_token_factory);
```

Emitted when old token factory address is replaced with new one.

### **`WithdrawTokens`**

```
WithdrawTokens(address vault_token_wallet, uint128 amount, address account_owner, address recipient_address);
```

### **`PairTransferTokens`**

```
PairTransferTokens(address vault_token_wallet, uint128 amount, address pair_left_root, address pair_right_root, address recipient_address);
```
