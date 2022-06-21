---
description: The DexAccount defines the logic for managing inside of the dex pool.
---

# DexAccount

Smart contract responsible for managing user transactions (withdraw/deposit tokens, withdraw/deposit liquidity, add pair, exchange) inside of the dex pool.

Derives following classes and interfaces: _DexContractBase, IDexAccount, IAcceptTokensTransferCallback, IUpgradableByRequest, IResetGas_

## Getters

### **`getRoot`**

Gets root address of the specific dex root.

```solidity
function getRoot() override external view responsible returns (address)
```

**Return values:**

| Type    | Description                           |
| ------- | ------------------------------------- |
| address | Address of the account's root address |

### **`getOwner`**

Gets the account owner.

```solidity
function getOwner() override external view responsible returns (address) 
```

**Return values:**

| Type    | Description                    |
| ------- | ------------------------------ |
| address | Address of the account’s owner |

### **`getVersion`**

Gets the current version of the account.

```solidity
function getVersion() override external view responsible returns (uint32)
```

**Return values**

| Type   | Description     |
| ------ | --------------- |
| uint32 | Current version |

### **`getVault`**

Gets the vault of the account.

```solidity
function getVault() override external view responsible returns (address)
```

**Return values:**

| Type    | Description          |
| ------- | -------------------- |
| address | Address of the vault |

### **`getWalletData`**

Use token\_root to check whether the specified token exists in wallets list, if it does returns wallet address and it’s balance, if not, returns 0 for address and balance respectively.

```solidity
function getWalletData(address token_root) override external view responsible returns (address wallet, uint128 balance)
```

****Parameters:****

| Name        | Type    | Description        |
| ----------- | ------- | ------------------ |
| token\_root | address | token root address |

| Name    | Type    | Description                            |
| ------- | ------- | -------------------------------------- |
| wallet  | address | Wallet address for the specified token |
| balance | uint128 | Token balance in the wallet            |

### **`getWallets`**

```solidity
function getWallets() external view returns (mapping(address => address))
```

Gets list of all the token wallets for this account.

**Return value:**

| Type    | Description                                                 |
| ------- | ----------------------------------------------------------- |
| address | List of all token wallets addresses for the certain account |

### **`getBalances`**

```solidity
function getBalances() external view returns (mapping(address => uint128))
```

Gets list of all the token balances for this account

**Return value:**

| Type    | Description                                                                     |
| ------- | ------------------------------------------------------------------------------- |
| uint128 | List of all token balances from different token wallets for the certain account |

## Deposit

### **`onAcceptTokensTransfer`** 

```solidity
function onAcceptTokensTransfer(address token_root, uint128 tokens_amount, address /* sender_address */, address sender_wallet, address original_gas_to, TvmCell payload) override external
```

If there is a wallet connected to this account for the specified token root then the transfer method is called from the TokenWallet (wallet will be deployed through that method), after which balance for specified token root is changed accordingly with the token amount to be deposited and all the balance left on the contract is transferred to sender’s token wallet contract address. If there isn’t specified token wallet connected to this account, then *transferToWallet* method is called from the TokenWallet to return tokens to the sender wallet(wallet must be deployed previously).

**Parameters:**

| Name            | Type    | Description                                             |
|-----------------|---------|---------------------------------------------------------|
| token_root      | address | Root address of a transferred token                     |
| tokens_amount   | uint128 | Amount of tokens being transferred                      |
| sender_address  | address | Address of the sender’s account                         |
| sender_wallet   | address | Address of the sender’s wallet                          |
| original_gas_to | address | Address of the receiver of remaining gas after transfer |
| payload         | TvmCell | Additional data referred to cancel action (need_cancel) |

## Withdraw

### **`withdraw`** 

```solidity
function withdraw(uint64  call_id, uint128 amount, address token_root, address recipient_address, uint128 deploy_wallet_grams, address send_gas_to) external
```

Does all the necessary checks for parameter value, reduces the balance for chosen token for the specified amount. Then it calls the TokenRoot method walletOf to get wallet address whose callback method is onVaultTokenWallet where the actual withdraw is happening through the DexVault.

**Parameters:**

| Name                | Type    | Description                                                 |
|---------------------|---------|-------------------------------------------------------------|
| call_id             | unit64  | Id of the operation call                                    |
| amount              | uint128 | Amount to withdraw                                          |
| token_root          | address | Token root address                                          |
| recipient_address   | address | Address of the recipient                                    |
| deploy_wallet_grams | uint128 | Amount of grams necessary to deploy a wallet                |
| send_gas_to         | address | Address where to send gas spent by calling contract methods |

## Transfers

### **`transfer`** 

```solidity
function transfer(uint64  call_id, uint128 amount, address token_root, address recipient, bool willing_to_deploy, address send_gas_to) override external onlyOwner
```

Reduces the transfer initiator’s token balance for the specified amount and builds data for the internalAccountTransfer method which is called next

**Parameters:**

| Name              | Type    | Description                                                 |
|-------------------|---------|-------------------------------------------------------------|
| call_id           | uint64  | ID of the operation call                                    |
| amount            | uint128 | Amount to transfer                                          |
| token_root        | address | Address of the token root                                   |
| to_dex_account    | address | Address of the dex account where to transfer tokens         |
| willing_to_deploy | bool    | True if yes, false if not                                   |
| send_gas_to       | address | Address where to send gas spent by calling contract methods |

### **`internalAccountTransfer`** 

```solidity
function internalAccountTransfer(uint64 call_id, uint128 amount, address token_root, address sender_owner, bool willing_to_deploy, address send_gas_to) external
```

Increases the recipient’s token balance and deploys recipient’s wallet for specified token if it doesn’t already exist, successCallback is called with a callId to notify that transfer succeeded. 

**Parameters:**

| Name              | Type    | Description                                               |
|-------------------|---------|-----------------------------------------------------------|
| call_id           | uint64  | ID of the operation call                                  |
| amount            | uint128 | Amount to transfer                                        |
| token_root        | address | Token root address                                        |
| sender_owner      | address | Address of the owner of sender’s account                  |
| willing_to_deploy | bool    | True if yes, false if not                                 |
| send_gas_to       | address | Address where to send gas when calling contract’s methods |

### **`internalPairTransfer`** 

```solidity
function internalPairTransfer(uint128 amount, address token_root, address sender_left_root, address sender_right_root, address send_gas_to) external
```

Increases the token’s balance of the specific pair token root in Dex Account, transfers it to it’s wallet and transfers all the remaining contract balance to send_gas_to address (send_gas_to.transfer(...)).

**Parameters:**

| Name              | Type    | Description                                               |
|-------------------|---------|-----------------------------------------------------------|
| amount            | uint128 | Amount to transfer                                        |
| token_root        | address | Token root address                                        |
| sender_left_root  | address | Left pair token’s root address                            |
| sender_right_root | address | Right pair token’s root address                           |
| send_gas_to       | address | Address where to send gas when calling contract’s methods |

## Pair operations 

Calling methods from the DexPair.

### **`exchange`**

```solidity
function exchange(uint64  call_id, uint128 spent_amount, address spent_token_root, address receive_token_root, uint128 expected_amount, address send_gas_to) override external onlyOwner
```

Does the checks for parameter values, reduces balance for the token root that is being spent for the specified spending amount and does the exchange through the DexPair

**Parameters:**

| Name               | Type    | Description                                               |
|--------------------|---------|-----------------------------------------------------------|
| call_id            | uint64  | ID of the operation call                                  |
| spent_amount       | uint128 | Amount given for the exchange                             |
| spent_token_root   | address | Token root address of the spent token in the exchange     |
| receive_token_root | address | Token root address of the received token in the exchange  |
| expected_amount    | uint128 | Expected amount of tokens to be received in the exchange  |
| send_gas_to        | address | Address where to send gas when calling contract’s methods |

### **`depositLiquidity`**

```solidity
function depositLiquidity(uint64  call_id, address left_root, uint128 left_amount, address right_root, uint128 right_amount, address expected_lp_root, bool auto_change, address send_gas_to) external
```

Does a lot of necessary checks for parameter values, reduces balance value on the account for both left and right root (for the amount that is being deposited) and deposits liquidity through the DexPair.

**Parameters:**

| Name             | Type    | Description                                                   |
|------------------|---------|---------------------------------------------------------------|
| call_id          | uint64  | Id of the operation call                                      |
| left_root        | address | Left token root address                                       |
| left_amount      | uint128 | Left token amount to deposit                                  |
| right_root       | address | Right token root address                                      |
| right_amount     | uint128 | Right token amount to deposit                                 |
| expected_lp_root | address | Address of the liquidity pool root where to deposit liquidity |
| auto_change      | bool    | If true automatically exchange right and left token           |
| send_gas_to      | address | Address where to send gas when calling contract’s methods     |

### **`withdrawLiquidity`**

```solidity 
function withdrawLiquidity(uint64  call_id, uint128 lp_amount, address lp_root, address left_root, address right_root, address send_gas_to) override external onlyOwner
```

Does the checks for parameter values, reduces balance in the liquidity pool for the amount that is being withdrawn and withdraws liquidity through the DexPair.

**Parameters:**

| Name        | Type    | Description                                               |
|-------------|---------|-----------------------------------------------------------|
| call_id     | uint64  | Id of the operation call                                  |
| lp_amount   | uint128 | Amount of lp tokens to withdraw from pool                 |
| lp_root     | address | Address of lp token root                                  |
| left_root   | address | Address of lp pool’s left token root                      |
| right_root  | address | Address of lp pool’s right token root                     |
| send_gas_to | address | Address where to send gas when calling contract’s methods |

## Wallets flow

### **`addPair`**

```solidity
function addPair(address left_root, address right_root) override external onlyOwner
```

Stores the virtual balance on the user's DexAccount and prepares some additional things for connecting this specific pair. It checks if this pair exists (if it is the correct pair or the malicious one) by calling checkPair method from the DexPair.

**Parameters:**

| Name       | Type    | Description                     |
|------------|---------|---------------------------------|
| left_root  | address | Left pair’s token root address  |
| right_root | address | Right pair’s token root address |

### **`checkPairCallback`**

```solidity
function checkPairCallback(address left_root, address right_root, address lp_root) override external onlyPair(left_root, right_root) 
```

Contains return value from the checkPair method and it’s deployed token wallets if they don’t exist, transfers all the contract’s balance to the owner’s address and ignores errors if they exist.

**Parameters:**

| Name       | Type    | Description                                     |
|------------|---------|-------------------------------------------------|
| left_root  | address | Left pair’s token root address                  |
| right_root | address | Right pair’s token root address                 |
| lp_root    | address | Address of the lp token root for the given pair |

### **`_deployWallet`**  

```solidity
function _deployWallet(address token_root, address send_gas_to) private
```

Deploys token wallet for the account owner through the TokenRoot method deployWallet whose callback method is onTokenWallet.

**Parameters:**

| Name        | Type    | Description                                               |
|-------------|---------|-----------------------------------------------------------|
| token_root  | address | Address of the token root                                 |
| send_gas_to | address | Address where to send gas when calling contract’s methods |

## Callback for ITokenRoot

### **`onTokenWallet`** 

```solidity
function onTokenWallet(address wallet) external
```

Adds wallet to the msg.sender’s address in the list of all the wallets and initialize balance if balance for deployed token wallet doesn’t exist, transfers all the contract’s balance to the send_gas_to address and ignores errors if they exist.

**Parameters:**

| Name   | Type    | Description                  |
|--------|---------|------------------------------|
| wallet | address | Address of the token wallet  |

### **`onVaultTokenWallet`** 

```solidity
function onVaultTokenWallet(address wallet) external
```

Does the necessary checks and calls the withdraw method from the DexVault where the actual withdrawal is happening, transfers all the contract’s balance to the send_gas_to address and ignores errors if they exist. 

**Parameters:**

| Name   | Type    | Description                    |
|--------|---------|--------------------------------|
| wallet | address | Address of the vault’s wallet  |

## Code upgrade

### **`upgrade`**  

```solidity
function upgrade(TvmCell code, uint32 new_version, address send_gas_to) override external onlyRoot
```

Upgrades account to a newer version and fills root, vault, owner, wallets, balances with new upgraded data, if current version is already newest version, transfers all the contract’s balance to the send_gas_to address and ignores errors if they exist.

**Parameters:**

| Name        | Type    | Description                                               |
|-------------|---------|-----------------------------------------------------------|
| code        | TvmCell | Code to be set for upgraded version                       |
| new_version | uint32  | New version value                                         |
| send_gas_to | address | Address where to send gas when calling contract’s methods |

### **`requestUpgrade`** 

```solidity
function requestUpgrade(address send_gas_to) external view onlyOwner
```

Emits CodeUpgradeRequested event and calls requestUpgradeAccount from DexRoot to request an upgrade.

**Parameters:**

| Name        | Type    | Description                                               |
|-------------|---------|-----------------------------------------------------------|
| send_gas_to | address | Address where to send gas when calling contract’s methods |

### **`onCodeUpgrade`** 

```solidity
function onCodeUpgrade(TvmCell upgrade_data) private
```

Callback function for code upgrade, it’s called from upgrade method, upgraded data is passed and it’s used for filling the necessary data from the new upgraded code. At the end, transfers all the contract’s balance to the send_gas_to address and ignores errors if they exist.

**Parameters:**

| Name         | Type    | Description                                                                                   |
|--------------|---------|-----------------------------------------------------------------------------------------------|
| upgrade_data | TvmCell | Cell containing all the data about certain DexAccount that should be replaced after upgrading |

## Success

### **`successCallback`**

```solidity
function successCallback(uint64 call_id) override external
```

Calls callback method dexAccountOnSuccess from the DexAccountOwner based on the send_gas_to address, if send_gas_to address is not owner’s address, transfers all the contract’s balance to the send_gas_to address and ignores errors if they exist.

**Parameters:**

| Name    | Type   | Description              |
|---------|--------|--------------------------|
| call_id | uint64 | Id of the operation call |

## Bounce

### **`onBounce`** 

```solidity
onBounce(TvmSlice body) external
```

Based on the function id passed through parameters, does the operation rollback and calls the dexAccountOnBounce method from the DexAccountOwner based on the send_gas_to address. If send_gas_to address is not owner’s address transfers all the contract’s balance to the send_gas_to address and ignores errors if they exist.

**Parameters:**

| Name | Type     | Description                                                                          |
|------|----------|--------------------------------------------------------------------------------------|
| body | TvmSlice | Contains data such as functionId and codeId used for determining the callback’s flow |

## Key Events

### **`WithdrawTokens`**

```solidity
WithdrawTokens(address root, uint128 amount, uint128 balance);
```

Emitted when tokens are withdrawn from an account

### **`TransferTokens`**

```solidity
TransferTokens(address root, uint128 amount, uint128 balance);
	
	Emitted when tokens are transferred to the account
```

### **`ExchangeTokens`**

```solidity
ExchangeTokens(address from, address to, uint128 spent_amount, uint128 expected_amount, uint128 balance);
```

Emitted during exchange of tokens

### **`DepositLiquidity`**

```solidity
DepositLiquidity(address left_root, uint128 left_amount, address right_root, uint128 right_amount, bool auto_change);
```

Emitted when depositing liquidity

### **`WithdrawLiquidity`**

```solidity
WithdrawLiquidity(uint128 lp_amount, uint128 lp_balance, address lp_root, address left_root, address right_root);
```

Emitted when withdrawing liquidity

### **`TokensReceived`**

```solidity
TokensReceived(address token_root, uint128 tokens_amount, uint128 balance, address sender_wallet);
```

Emitted when transferring tokens

```solidity
TokensReceivedFromAccount
TokensReceivedFromAccount(address token_root, uint128 tokens_amount, uint128 balance, address sender);
```

Emitted when internal account transfer occurs

### **`TokensReceivedFromPair`**

```solidity
TokensReceivedFromPair(address token_root, uint128 tokens_amount, uint128 balance, address left_root, address right_root);
```

Emitted when internal pair transfer occurs

### **`OperationRollback`**

```solidity
OperationRollback(address token_root, uint128 amount, uint128 balance, address from);
```

Emitted inside onBounce callback

### **`ExpectedPairNotExist`**

```solidity
ExpectedPairNotExist(address pair);
```

Emitted inside onBounce callback

### **`AccountCodeUpgraded`**

```solidity
AccountCodeUpgraded(uint32 version);
```

Emitted when account is upgraded

### **`CodeUpgradeRequested`**

```solidity
CodeUpgradeRequested();
```
Emitted when requesting upgrade

