---
description: This smart contract defines the logic for managing exchange, cross pair exchange and deposit/withdraw liquidity inside the pair’s pool.
---

# DexPair

Smart contract of the dex pair responsible for managing exchange, cross pair exchange, deposit/withdraw liquidity inside the pair’s pool.

Derives following classes and interfaces: <u>*DexContractBase, IDexPair, IAcceptTokensTransferCallback, IUpgradableByRequest, IResetGas, ITokenOperationStructure.*</u>

## Getters

### **`getRoot`** 

```
function getRoot() override external view responsible returns (address dex_root)
```

Returns address of the current Dex root.

**Return values:**

| Name     | Type    | Description                        |
|----------|---------|------------------------------------|
| dex_root | address | Address of the pair’s root address |

### **`getTokenRoots`** 

```
function getTokenRoots() override external view responsible returns (address left, address right, address lp)
```

Returns left, right root and liquidity pool root address.

**Return values:**

| Name  | Type    | Description                            |
|-------|---------|----------------------------------------|
| left  | address | Address of the pair’s left token root  |
| right | address | Address of the pair’s right token root |
| lp    | address | Address of the liquidity pool root     |

### **`getTokenWallets`** 

```
function getTokenWallets() override external view responsible returns (address left, address right, address lp)
```

Returns left, right and liquidity pool wallet address.

**Return values:**

| Name  | Type    | Description                          |
|-------|---------|--------------------------------------|
| left  | address | Address of the wallet’s left token   |
| right | address | Address of the wallet’s right token  |
| lp    | address | Address of the liquidity pool wallet |

### **`getVersion`** 

```
function getVersion() override external view responsible returns (uint32 version)
```

Returns current version of the dex pair.

**Return values:**

| Name    | Type   | Description     |
|---------|--------|-----------------|
| version | uint32 | Current version |

### **`getVault`** 

```
function getVault() override external view responsible returns (address dex_vault)
```

Returns the vault of the desired dex pair.

**Return values:**

| Name      | Type    | Description               |
|-----------|---------|---------------------------|
| dex_vault | address | Vault address of dex pair |

### **`getVaultWallets`** 

```
function getVaultWallets() override external view responsible returns (address left, address right)
```

Returns left and right vault wallet addresses.

**Return values:**

| Name  | Type    | Description                             |
|-------|---------|-----------------------------------------|
| left  | address | Vault address of the left pair’s token  |
| right | address | Vault address of the right pair’s token |

### **`setFeeParams`** 

```
function setFeeParams(uint16 numerator, uint16 denominator) override external onlyRoot
```

Sets fees based on the numerator and denominator and emits FeesParamsUpdated to notify that new fees were set.

**Parameters:**

| Name        | Type   | Description                        |
|-------------|--------|------------------------------------|
| numerator   | uint16 | Numerator value for setting fees   |
| denominator | uint16 | Denominator value for setting fees |

### **`getFeeParams`** 

```
function getFeeParams() override external view responsible returns (uint16 numerator, uint16 denominator)
```

Returns fee numerator and denominator

**Return values:**

| Name        | Type   | Description       |
|-------------|--------|-------------------|
| numerator   | uint16 | Numerator value   |
| denominator | uint16 | Denominator value |

### **`isActive`** 

```
function isActive() override external view responsible returns (bool)
```

Checks whether the DexPair account is active, returns true if yes, false if not.

**Return values:**

| Type | Description                   |
|------|-------------------------------|
| bool | DexPair account active or not |

### **`getBalances`** 

```
function getBalances() override external view responsible returns (IDexPairBalances)
```

Returns liquidity pool supply and left and right balance.

**Return values:**

| Type             | Description                |
|------------------|----------------------------|
| IDexPairBalances | Pair’s balance information |

## Direct operations

### **`buildExchangePayload`** 

```
function buildExchangePayload(uint64 id, uint128 deploy_wallet_grams, uint128 expected_amount) external pure returns (TvmCell)
```

Builds the payload data for the exchange operation and converts it to cell.

**Parameters:**

| Name                | Type     | Description                                     |
|---------------------|----------|-------------------------------------------------|
| id                  | uint64   | Id of the operation call                        |
| deploy_wallet_grams | uint128  | Fee for deploying wallet                        |
| expected_amount     | uint128  | Expected amount of receive token after exchange |

**Return values:**

| Type    | Description                      |
|---------|----------------------------------|
| TvmCell | Payload data needed for exchange |

### **`buildDepositLiquidityPayload`**

```
function buildDepositLiquidityPayload(uint64 id, uint128 deploy_wallet_grams) external pure returns (TvmCell)
```

Builds the payload data for the deposit liquidity operation and converts it to cell.

**Parameters:**

| Name                | Type     | Description              |
|---------------------|----------|--------------------------|
| id                  | uint64   | Id of the operation call |
| deploy_wallet_grams | uint128  | Fee for deploying wallet |

**Return values:**

| Type    | Description                                       |
|---------|---------------------------------------------------|
| TvmCell | Payload data needed for deposit to liquidity pool |

### **`buildWithdrawLiquidityPayload`** 

```
function buildWithdrawLiquidityPayload(uint64 id, uint128 deploy_wallet_grams) external pure returns (TvmCell)
```

Builds the payload data for the withdraw liquidity operation and converts it to cell.

**Parameters:**

| Name                | Type     | Description              |
|---------------------|----------|--------------------------|
| id                  | uint64   | Id of the operation call |
| deploy_wallet_grams | uint128  | Fee for deploying wallet |

**Return values:**

| Type    | Description                                            |
|---------|--------------------------------------------------------|
| TvmCell | Payload data needed for withdrawal from liquidity pool |

### **`buildCrossPairExchangePayload`** 

```
function buildCrossPairExchangePayload(uint64 id, uint128 deploy_wallet_grams, uint128 expected_amount, TokenOperation[] steps) external pure returns (TvmCell)
```

Builds the payload data for the cross-pair exchange operation and converts it to cell.

**Parameters:**

| Name                | Type             | Description                                     |
|---------------------|------------------|-------------------------------------------------|
| id                  | uint64           | Id of the operation call                        |
| deploy_wallet_grams | uint128          | Fee for deploying wallet                        |
| expected_amount     | uint128          | Expected amount of receive token after exchange |
| steps               | TokenOperation[] | Next pairs for exchange                         |
	
**Return values:**

| Type    | Description                                 |
|---------|---------------------------------------------|
| TvmCell | Payload data needed for cross-pair exchange |

### **`onAcceptTokenTransfer`**

```
function onAcceptTokensTransfer(address token_root, uint128 tokens_amount, address sender_address, address sender_wallet, address original_gas_to, TvmCell payload) override external
```

Changes values of contract’s data such as left balance, right balance, liquidity pool supply etc. according to the operation that is related to the token transfer such as: Deposit liquidity, Exchange, Cross pair exchange and according to the operations flows (right to left/left to right).  
Depending on the operation success callbacks are called and proper events are emitted.  
If any of the operations are canceled, tokens used in transfer are burned and cancel callbacks and events are called.

**Parameters:**

| Name            | Type     | Description                                               |
|-----------------|----------|-----------------------------------------------------------|
| token_root      | address  | Token root address of the token that is transferred       |
| tokens_amount   | uint128  | Amount of the token to be transferred                     |
| sender_address  | address  | Address of the sender account                             |
| sender_wallet   | address  | Sender’s wallet address                                   |
| original_gas_to | address  | Address where to send gas when calling contract’s methods |
| payload         | TvmCell  | Additional data about transaction flow                    |

## Deposit liquidity

### **`expectedDepositLiquidity`** 

```
function expectedDpositLiquidity(uint128 left_amount, uint128 right_amount, bool auto_change) override external view responsible returns (DepositLiquidityResult)
```

### **`expectedDepositLiquidity`** 

```
function expectedDpositLiquidity(uint128 left_amount, uint128 right_amount, bool auto_change) override external view responsible returns (DepositLiquidityResult)
```

Called before depositing liquidity in order to calculate the expected deposit liquidity.
- If liquidity supply is 0 create DepositLiquidityResult with left amount, right amount, max value of left and right amountl.
- Else calculate it by calling `_expectedDepositLiquidity`.

**Parameters:**

| Name         | Type    | Description                                |
|--------------|---------|--------------------------------------------|
| left_amount  | uint128 | Left token amount in liquidity pool        |
| right_amount | uint128 | Right token amount in liquidity pool       |
| auto_change  | bool    | If true automatically deposit to liquidity |

**Return values:**

| Type                   | Description |
|------------------------|-------------|
| DepositLiquidityResult |             |

### **`_expectedDepositLiquidity`** 

```
function _expectedDepositLiquidity(uint128 left_amount, uint128 right_amount, bool auto_change) private view returns (DepositLiquidityResult)
```

Does the actual calculation for expected deposit liquidity and returns deposit liquidity result.   
If the left and right amount for depositing are greater than 0, calculate the first deposit for the left and right token and liquidity pool reward and after that calculate current left, right balance and lp supply in order to either continue with the exchange if they are greater than 0, or create deposit results right away.  
When all checks are done and all values are calculated, DepositLiquidityResult is built and returned as expected.

**Parameters:**

| Name         | Type    | Description                                |
|--------------|---------|--------------------------------------------|
| left_amount  | uint128 | Left token amount in liquidity pool        |
| right_amount | uint128 | Right token amount in liquidity pool       |
| auto_change  | bool    | If true automatically deposit to liquidity |

**Return values:**

| Type                   | Description                      |
|------------------------|----------------------------------|
| DepositLiquidityResult | Deposit to liquidity pool result |

### **`depositLiquidity`** 

```
function depositLiquidity(uint64 call_id, uint128 left_amount, uint128 right_amount, address expected_lp_root, bool auto_change, address account_owner, uint32 /*account_version*/, address send_gas_to ) override external onlyActive onlyAccount(account_owner)
```

Calculates and stores data such as liquidity pool supply, left balance, right balance and if it is first deposit to the current pool calls dexPairDepositLiquiditySuccess callback. If not, according to the data retrieved calling `_expectedDepositLiquidity` changes left and right balance values, calls DexAccount’s InternalPairTransfer if there is need for exchange.   
When everything is successfully done, mint is started in the dex pair’s root where recipient is account owner and successCallback is called to notify about successful deposit action.

**Parameters:**

| Name             | Type     | Description                                               |
|------------------|----------|-----------------------------------------------------------|
| call_id          | uint64   | ID of the operation call                                  |
| left_amount      | uint128  | Left token amount to be deposited in the liquidity pool   |
| right_amount     | uint128  | Right token amount to be deposited in the liquidity pool  |
| expected_lp_root | address  | Root address of the liquidity pool used for depositing    |
| auto_change      | bool     | If true automatically deposit right and left token        |
| account_owner    | address  | Address of the account’s owner                            |
| account_version  | uint32   | Current version of the account                            |
| send_gas_to      | address  | Address where to send gas when calling contract’s methods |

## Withdraw liquidity

### **`_withdrawLiquidityBase`** 

```
function _withdrawLiquidityBase(uint128 lp_amount) private returns (uint128, uint128)
```

Reduces right and left balance for the amount that is being withdrawn and reduces the liquidity pool supply for the total value of withdrawal, emits WithdrawLiquidity with lp amount withdrawn and left and right amount taken from the pool.

**Parameters:**

| Name      | Type    | Description                                    |
|-----------|---------|------------------------------------------------|
| lp_amount | uint128 | Amount to be withdrawn from the liquidity pool |

**Return values:**

| Type     | Description                               |
|----------|-------------------------------------------|
| uint128  | Amount of the left token to be withdrawn  |
| uint128  | Amount of the right token to be withdrawn |

### **`expectedWithdrawLiquidity`** 

```
function expectedWithdrawLiquidity(uint128 lp_amount) override external view responsible returns (uint128 expected_left_amount, uint128 expected_right_amount)
```

Calculates the left and right amount to be withdrawn based on the total value that is requested to be withdrawn.

**Parameters:**

| Name      | Type                                      | Description                                    |
|-----------|-------------------------------------------|------------------------------------------------|
| lp_amount | uint128                                   | Amount to be withdrawn from the liquidity pool |
| uint128   | Amount of the right token to be withdrawn |                                                |

**Return values:**

| Name                  | Type     | Description                                                           |
|-----------------------|----------|-----------------------------------------------------------------------|
| expected_left_amount  | uint128  | Calculated left token amount to be withdrawn from the liquidity pool  |
| expected_right_amount | uint128  | Calculated right token amount to be withdrawn from the liquidity pool |

### **`withdrawLiquidity`** 

```
function withdrawLiquidity(uint64 call_id, uint128 lp_amount, address expected_lp_root, address account_owner, uint32 /*account_version*/, address send_gas_to) override external onlyActive onlyAccount(account_owner)
```

Calculating and applying new liquidity pool balances and supply after withdrawal, transferring withdrawn amount to DexAccount. If initial required conditions are fulfilled, get left and right amount of tokens to withdraw by calling `_withdrawLiquidityBase`, call dexPairWithdrawSuccess callback for account owner to notify successful withdrawal.  
If left and right amount to withdraw are greater than 0 transfer them to the account by calling DexAccount’s internalPairTransfer, burn withdrawn tokens in the specified pool by calling burnTokens method from the `IBurnableByRootTokenRoot`.

**Parameters:**

| Name             | Type     | Description                                               |
|------------------|----------|-----------------------------------------------------------|
| call_id          | uint64   | ID of the operation call                                  |
| lp_amount        | uint128  | Amount to be withdrawn from the liquidity pool            |
| expected_lp_root | address  | Root address of the liquidity pool used for withdrawal    |
| account_owner    | address  | Address of the account’s owner                            |
| account_version  | uint32   | Current version of the account                            |
| send_gas_to      | address  | Address where to send gas when calling contract’s methods |

## Exchange

### **`expectedExchange`** 

```
function expectedExchange(uint128 amount, address spent_token_root) override external view responsible returns (uint128 expected_amount, uint128 expected_fee)
```

Returns the expected exchange amount and exchange fee based on the amount to exchange and token used for exchange by calling the private method `_expectedExchange`.

**Parameters:**

| Name             | Type     | Description                                       |
|------------------|----------|---------------------------------------------------|
| amount           | uint128  | Token amount to be exchanged                      |
| spent_token_root | address  | Address of the token root which will be exchanged |

**Return values:**

| Name            | Type     | Description                 |
|-----------------|----------|-----------------------------|
| expected_amount | uint128  | Calculated exchange amount  |
| expected_fee    | uint128  | Calculated exchange fee     |

expectedSpendAmount 

```
function expectedSpendAmount(uint128 receive_amount, address receive_token_root) override external view responsible returns (uint128 expected_amount, uint128 expected_fee)
```

Returns the expected spend amount and expected fee by calling the private method `_expectedSpendAmount` based on receive amount and specified token root address

**Parameters:**

| Name               | Type     | Description                                        |
|--------------------|----------|----------------------------------------------------|
| receive_amount     | uint128  | Token amount to receive after exchange             |
| receive_token_root | address  | Token root address of the receiving exchange token |

**Return values:**

| Name            | Type    | Description                   |
|-----------------|---------|-------------------------------|
| expected_amount | uint128 | Calculated amount to be spent |
| expected_fee    | uint128 | Calculated fee                |

exchange 

```
function exchange(uint64 call_id, uint128 spent_amount, address spent_token_root, address receive_token_root, uint128 expected_amount, address account_owner, uint32 /*account_version*/, address send_gas_to) override external onlyActive onlyAccount(account_owner)
```

Swap function between tokens of one liquidity pool, checks in which direction the exchange is initiated and if all the conditions are fulfilled (enough tokens, fees greater than 0, send amount ge expected amount…) balance on sender token side will decrease and balance on the receiver token side will increase.

**Parameters:**

| Name               | Type     | Description                                                    |
|--------------------|----------|----------------------------------------------------------------|
| call_id            | uint64   | ID of the operation call                                       |
| spent_amount       | uint128  | Amount of the spend token to be exchanged for receive token    |
| spent_token_root   | address  | Address of the token which will be exchanged for receive token |
| receive_token_root | address  | Address of the token for which exchange is happening           |
| expected_amount    | uint128  | Expected amount of the receive token                           |
| account_owner      | address  | Address of the account which is the exchange initiator         |
| account_version    | uint32   | Current version of the account                                 |
| send_gas_to        | address  | Address where to send gas when calling contract’s methods      |

_expectedExchange 

```
function _expectedExchange(uint128 a_amount, uint128 a_pool, uint128 b_pool) private view returns (uint128, uint128)
```

Does the actual calculation for the desired exchange, calculates exchange fee, returns  amount of tokens that are exchanged calculated by a special equation and fee for the given exchange token.

**Parameters:**

| Name     | Type    | Description                       |
|----------|---------|-----------------------------------|
| a_amount | uint128 | Token amount to be exchanged      |
| a_pool   | uint128 | Total amount of left/right tokens |
| b_pool   | uint128 | Total amount of right/left tokens |

| Type     | Description                        |
|----------|------------------------------------|
| uint128  | Token amount to get after exchange |
| uint128  | Exchange fee                       |

_expectedSpendAmount 

```
function _expectedSpendAmount(uint128 b_amount, uint128 a_pool, uint128 b_pool) private view returns (uint128, uint128)
```

Calculates the expected spending amount based on the tokens amount that will be taken from exchange, total amount of tokens in the pool of the token that will be given for exchange and total amount of tokens in the pool from which desired tokens will be taken, returns expected amount of tokens that will be given for an exchange and fee for exchange.

**Parameters:**

| Name     | Type    | Description                        |
|----------|---------|------------------------------------|
| b_amount | uint128 | Token amount to get after exchange |
| a_pool   | uint128 | Total amount of left/right tokens  |
| b_pool   | uint128 | Total amount of right/left tokens  |

**Return values:**

| Type     | Description               |
|----------|---------------------------|
| uint128  | Token amount to  exchange |
| uint128  | Exchange fee              |

## Cross-pair exchange

crossPairExchange

```
function crossPairExchange( uint64 id, uint32 /*prev_pair_version*/, address prev_pair_left_root, address prev_pair_right_root, address spent_token_root, uint128 spent_amount, address sender_address, address original_gas_to, uint128 deploy_wallet_grams, TvmCell payload) override external onlyPair(prev_pair_left_root, prev_pair_right_root) onlyActive
```

Checks whether the exchange is happening between pairs of different liquidity pools or between tokens in the same liquidity pool, if it is between lps crossPairExchange is called and if it’s inside of one lp the DexVault’s transfer function is called. If the conditions such as sufficient balance, fees > 0 etc. are not fulfilled, operation is canceled.

**Parameters:**

| Name                 | Type     | Description                                                      |
|----------------------|----------|------------------------------------------------------------------|
| id                   | uint64   | ID of the operation call                                         |
| prev_pair_version    | uint32   | Current version of the first pair of the cross exchange          |
| prev_pair_left_root  | address  | Left token root address of the first pair of the cross exchange  |
| prev_pair_right_root | address  | Right token root address of the first pair of the cross exchange |
| spent_token_root     | address  | Token root address which will be exchanged                       |
| spent_amount         | uint128  | Amount of the token to be exchanged                              |
| sender_address       | address  | Address of the account which is the cross exchange initiator     |
| original_gas_to      | address  | Address where to send gas when calling contract’s methods        |
| deploy_wallet_grams  | uint128  | Fee for deploying wallet                                         |
| payload              | TvmCell  | Additional data about next exchange in row                       |

## Account operations

checkPair 

```
function checkPair(address account_owner, uint32 /*account_version*/) override external onlyAccount(account_owner)
```

Calls DexAccount’s checkPairCallbeck to check weather the pair exists if not, deploys wallets for each side of the token pair and lp root if it doesn’t exist.

**Parameters:**

| Name            | Type    | Description                                            |
|-----------------|---------|--------------------------------------------------------|
| account_owner   | address | Address of the account which is the exchange initiator |
| account_version | uint32  | Current version of the account                         |

## Code upgrade

upgrade 

```
function upgrade(TvmCell code, uint32 new_version, address send_gas_to) override external onlyRoot
```

Upgrades pair to a newer version and builds tokens, liquidity tokens, balances, fees, wallets, vault wallets with new upgraded data, calls onCodeUpgrade from new code

**Parameters:**

| Name        | Type     | Description                                               |
|-------------|----------|-----------------------------------------------------------|
| code        | TvmCell  | Code to be set for upgraded version                       |
| new_version | uint32   | New version value                                         |
| send_gas_to | address  | Address where to send gas when calling contract’s methods |

onCodeUpgrade 

```
function onCodeUpgrade(TvmCell upgrade_data) private
```

Private method used in Upgrade, resets storage, creates new TvmSlice instance and fills it by calling `upgrade_data`, loads and decodes from slice data such as left, right root, vault address, root address, old version number, current version, send gas to address, after that checks if old version is 0 
- If it is, initializes fee params, adds liquidity to a new dex pair by calling DexVault’s addLiquidityToken.
- If not sets pool to active, load and decodes lp supply, left, right balance, fee params, lp wallet, left and right wallet and vault’s left and right wallet

**Parameters:**

| Name         | Type    | Description                                                                                   |
|--------------|---------|-----------------------------------------------------------------------------------------------|
| upgrade_data | TvmCell | Cell containing all the data about certain DexAccount that should be replaced after upgrading |

_configureTokenRootWallets 

```
function _configureTokenRootWallets(address token_root) private view
```

Using address deploys new wallet and if token root is not equal to the lp root return wallet whose owner is vault.

**Parameters:**

| Name       | Type    | Description               |
|------------|---------|---------------------------|
| token_root | address | Address of the token root |

onTokenWallet 

```
function onTokenWallet(address wallet) external
```

Configure wallet based on the sender’s role (left root/right root/lp root) and if non of the wallets included in the lp pool are empty set wallet to active.

**Parameters:**

| Name   | Type    | Description                 |
|--------|---------|-----------------------------|
| wallet | address | Address of the token wallet |

onVaultTokenWallet

```
function onVaultTokenWallet(address wallet) external
```

If sender is either right or left root and based on which root it is if one of those vault wallets are not configured, the wallet address from the function params will be passed as vault wallet address.

**Parameters:**

| Name   | Type    | Description                    |
|--------|---------|--------------------------------|
| wallet | address | Address of the vault’s wallet  |

liquidityTokenRootDeployed 

```
function liquidityTokenRootDeployed(address lp_root_, address send_gas_to) override external onlyVault
```

Configures token root wallets for lp root, left token root and right token root, calls DexRoot’s onPairCreated callback that notifies that the pair is created.

**Parameters:**

| Name        | Type    | Description                                               |
|-------------|---------|-----------------------------------------------------------|
| lp_root_    | address | Address of the liquidity pool                             |
| send_gas_to | address | Address where to send gas when calling contract’s methods |

liquidityTokenRootNotDeployed 

```
function liquidityTokenRootNotDeployed(address /*lp_root_*/, address send_gas_to) override external onlyVault
```

Returns gas to the deployer address, it is used by DexVault’s `onLiquidityTokenNotDeployed`.

**Parameters:**

| Name        | Type    | Description                                               |
|-------------|---------|-----------------------------------------------------------|
| lp_root_    | address | Address of the liquidity pool                             |
| send_gas_to | address | Address where to send gas when calling contract’s methods |

## Key Events

### **`PairCodeUpgraded`**

```
PairCodeUpgraded(uint32 version);
```

Emitted when pair code upgrades.

### **`FeesParamsUpdated`**

```
FeesParamsUpdated(uint16 numerator, uint16 denominator);
```

Emitted when numerator and denominator value gets updated.

### **`DepositLiquidity`**

```
DepositLiquidity(uint128 left, uint128 right, uint128 lp);
```

Emitted when liquidity is deposited.

### **`WithdrawLiquidity`**

```
WithdrawLiquidity(uint128 lp, uint128 left, uint128 right);
```

Emitted when withdrawing liquidity.

### **`ExchangeLeftToRight`**

```
ExchangeLeftToRight(uint128 left, uint128 fee, uint128 right);
```

Emitted whenever left token to right token exchange occurs.

### **`ExchangeRightToLeft`**

```
ExchangeRightToLeft(uint128 right, uint128 fee, uint128 left);
```

Emitted whenever right token to left token exchange occurs.
