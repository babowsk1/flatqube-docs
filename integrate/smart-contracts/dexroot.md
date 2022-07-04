---
description: The DexRoot logic is used for deploying and updating pairs and accounts. Also it is used to  set account/pair codes and other data related to the pairs and accounts such as vault and owner address.
---

# DexRoot

Smart contract responsible for deploying and updating pairs and accounts, setting account/pair codes and other data related to the pairs and accounts such as vault and owner address. Gets version of account/pair.

Derives following classes and interfaces:   
<u>*DexContractBase, IDexRoot, IResetGas, IUpgradable*</u>


### **Contains `constructor` with params**

```
constructor(address initial_owner, address initial_vault) public
```

Used for filling the data about new DexRoot.

**Parameters:**

| Name          | Type     | Description                                          |
|---------------|----------|------------------------------------------------------|
| initial_owner | address  | Address of the first owner of the current dex root   |
| initial_vault | address  | Address of the initial vault of the current dex root |

### **`_dexRoot`**

```
function _dexRoot() override internal view returns(address)
```

Returns address of the current DexRoot.

**Return Value:**

| Type     | Description                     |
|----------|---------------------------------|
| address  | Address of the current dex root |

### **`installPlatformOnce`** 

```
function installPlatformOnce(TvmCell code) external onlyOwner
```

Fills data for creating new platform for DexRoot, sets platform code.

**Parameters:**

| Name | Type    | Description                                |
|------|---------|--------------------------------------------|
| code | TvmCell | Platform code to be set for initialization |

### **`installOrUpdateAccountCode`**

```
function installOrUpdateAccountCode(TvmCell code) external onlyOwner
```

Uses the code parameter as the account code and if it’s not installed yet installs it.  
If it is, updates it.

**Parameters:**

| Name | Type    | Description                             |
|------|---------|-----------------------------------------|
| code | TvmCell | Account code to be set for this version |

### **`installOrUpdatePairCode`**

```
function installOrUpdatePairCode(TvmCell code) external onlyOwner
```

Uses the code parameter as the pair code and if it’s not installed yet installs it.  
If it is, updates it.

**Parameters:**

| Name | Type    | Description                          |
|------|---------|--------------------------------------|
| code | TvmCell | Pair code to be set for this version |
|      |         | version                              |

### **`getAccountVersion`**

```
function getAccountVersion() override external view responsible returns (uint32)
```

Gets the current version of the account.

**Return Value:**

| Type   | Description     |
|--------|-----------------|
| uint32 | Account version |

### **`getPairVersion`**

```
function getPairVersion() override external view responsible returns (uint32)
```

Gets the current version of the desired pair.

**Return Value:**

| Type   | Description  |
|--------|--------------|
| uint32 | Pair version |

## Vault

### **`setVaultOnce`** 

```
function setVaultOnce(address new_vault) external onlyOwner
```

Sets the vault of the DexRoot, passed vault’s address value must be zero in order to be set, it’s done only once per new root.

**Parameters:**

| Name      | Type     | Description                    |
|-----------|----------|--------------------------------|
| new_vault | address  | Address of the vault to be set |

### **`getVault`** 

```
function getVault() override external view responsible returns (address)
```

Gets the vault of the desired DexRoot.

**Return Value:**

| Type    | Description                 |
|---------|-----------------------------|
| address | Address of the root’s vault |

## Active

### **`setActive`** 

```
function setActive(bool new_active) external onlyOwner
```

Checks the conditions such as is the newActive parameter true, vault is already set, account and pair versions are set, if all the conditions are fulfilled DexRoot is set to active.   
After the active variable is set, ActiveUpdated event is emitted and contract’s balance is transferred to the owner’s account.

**Parameters:**

| Name       | Type | Description                                                                  |
|------------|------|------------------------------------------------------------------------------|
| new_active | bool | Decides weather the root will be active or not, active if true, not if false |

### **`isActive`** 

```
function isActive() override external view responsible returns (bool)
```

Checks whether the DexRoot account is active, returns true if yes, false if not.

**Return Value:**

| Type | Description                              | Description                                                                  |
|------|------------------------------------------|------------------------------------------------------------------------------|
| bool | True if the root is active, false if not | Decides weather the root will be active or not, active if true, not if false |

## Upgrade

### **`upgrade`** 

```
function upgrade(TvmCell code) override external onlyOwner
```

Upgrades root contract to a newer version, emits RootCodeUpgraded event, creates new TvmBuilder instance and stores required params for upgrade, sets new code and calls `onCodeUpgrade` callback to finish with upgrade.

**Parameters:**

| Name | Type    | Description                         |
|------|---------|-------------------------------------|
| code | TvmCell | Code to be set for upgraded version |

### **`requestUpgradeAccount`** 

```
function requestUpgradeAccount(uint32 current_version, address send_gas_to, address account_owner) external
```

Using accountOwner and `send_gas_to` addresses and current_version parameter upgrades account if it’s not already upgraded to the latest version, calling `UpgradableByRequest`’s upgrade method.

**Parameters:**

| Name            | Type    | Description                                                 |
|-----------------|---------|-------------------------------------------------------------|
| current_version | uint32  | Desired version for upgrade                                 |
| send_gas_to     | address | Address where to send gas spent by calling contract methods |
| account_owner   | address | Address of the owner whose account should be upgraded       |

### **`forceUpgradeAccount`** 

```
function forceUpgradeAccount(address account_owner, address send_gas_to)
```

Upgrades account to the latest version using account owner and `send_gas_to` addresses, emits `RequestedForceAccountUpgrade` event.

**Parameters:**

| Name          | Type     | Description                                                 |
|---------------|----------|-------------------------------------------------------------|
| account_owner | address  | Account owner address                                       |
| send_gas_to   | address  | Address where to send gas spent by calling contract methods |

### **`upgradePair`**
 
``` 
function upgradePair(address left_root, address right_root, address send_gas_to) external view onlyOwner
```

According to the leftRoot, rightRoot and `send_gas_to` address parameters upgrades left and right pair and emits  `RequestedPairUpgrade` event.

**Parameters:**

| Name        | Type     | Description                                                 |
|-------------|----------|-------------------------------------------------------------|
| left_root   | address  | Root address of the left pair                               |
| right_root  | address  | Root address of the right pair                              |
| send_gas_to | address  | Address where to send gas spent by calling contract methods |

## Reset

### **`resetGas`** 

```
function resetGas(address receiver) override external view onlyOwner
```
Resets balance to `ROOT_INITIAL_BALANCE`.

**Parameters:**

| Name     | Type     | Description                                                 |
|----------|----------|-------------------------------------------------------------|
| receiver | address  | Address where to send gas spent by calling contract methods |
|          |          | spent by calling contract methods                           |

### **`resetTargetGas`** 

```
function resetTargetGas(address target, address receiver) external view onlyOwner
```

Calculates value for gas to be reset at and after that resets gas to calculated value for target address calling IResetGas’s resetGas method.

**Parameters:**

| Name     | Type     | Description                                                 |
|----------|----------|-------------------------------------------------------------|
| target   | address  | Address for which gas should be reset                       |
| receiver | address  | Address where to send gas spent by calling contract methods |

## Owner

### **`getOwner`** 

```
function getOwner() external view responsible returns (address dex_owner)
```

Returns owner’s address.

**Return Value:**

| Name      | Type     | Description                 |
|-----------|----------|-----------------------------|
| dex_owner | address  | Address of the root’s owner |

### **`getPendingOwner`** 

```
function getPendingOwner() external view responsible returns (address dex_pending_owner)
```

Returns pending owner’s address.

**Return Value:**

| Name              | Type     | Description                         |
|-------------------|----------|-------------------------------------|
| dex_pending_owner | address  | Address of the root’s pending owner |

### **`transferOwner`** 

```
function transferOwner(address new_owner) external onlyOwner
```

Pending owner address gets value of the new owner param which is used in acceptOwner method (where actual transfer of ownership is happening) and emits `RequestedOwnerTransfer` event.

**Parameters:**

| Name      | Type     | Description                      |
|-----------|----------|----------------------------------|
| new_owner | address  | Address of the new pending owner |

### **`acceptOwner`** 

```
function acceptOwner() external
```

Accepts new owner in a way that owner becomes pending owner and emits `OwnerTransferAccepted` event.

## Expected address functions

### **`getExpectedAccountAddress`** 

```
function getExpectedAccountAddress(address account_owner) external view responsible returns (address)
```

Calls `_expectedAccountAddress` and based on account owner’s address returns expected address.

**Parameters:**

| Name          | Type    | Description                    |
|---------------|---------|--------------------------------|
| account_owner | address | Address of the account’s owner |

**Return Value:**

| Type    | Description                |
|---------|----------------------------|
| address | Expected account’s address |

### **`getExpectedPairAddress`**

```
function getExpectedPairAddress(address left_root, address right_root) override external view responsible returns (address)
```

Calls `_expectedPairAddress` and based on left and right root’s addresses returns expected pair address.

**Parameters:**

| Name       | Type    | Description                            |
|------------|---------|----------------------------------------|
| left_root  | address | Address of the left pair’s token root  |
| right_root | address | Address of the right pair’s token root |

**Return Value:**

| Type    | Description             |
|---------|-------------------------|
| address | Expected pair’s address |

## Deploy

### **`deployAccount`** 

```
function deployAccount(address account_owner, address send_gas_to) external 
```

Used for deploying child contracts, creates new DexPlatform for the account and passes data such as account code, version, vault address and address for receiving gas for new root that needs to be deployed.

**Parameters:**

| Name          | Type    | Description                                                 |
|---------------|---------|-------------------------------------------------------------|
| account_owner | address | Address of the account’s owner                              |
| send_gas_to   | address | Address where to send gas spent by calling contract methods |

### **`deployPair`** 

```
function deployPair(address left_root, address right_root, address send_gas_to) external
```

Creates new DexPlatform for the pair and passes data for a new pair that needs to be deployed.

**Parameters:**

| Name        | Type    | Description                                                 |
|-------------|---------|-------------------------------------------------------------|
| left_root   | address | Address of the left pair’s token root                       |
| right_root  | address | Address of the right pair’s token root                      |
| send_gas_to | address | Address where to send gas spent by calling contract methods |

### **`onPairCreated`** 

```
function onPairCreated(address left_root, address right_root, address send_gas_to) override external onlyPair(left_root, right_root)
```

Callback method, based on `right_root` and `left_root` params notify that the new pair is created and transfer fees.

**Parameters:**

| Name        | Type     | Description                                                 |
|-------------|----------|-------------------------------------------------------------|
| left_root   | address  | Root address of the left pair                               |
| right_root  | address  | Root address of the right pair                              |
| send_gas_to | address  | Address where to send gas spent by calling contract methods |

## Key Events

### **`AccountCodeUpgraded`**

```
AccountCodeUpgraded(uint32 version);
```

Emitted when account code is upgraded

### **`PairCodeUpgraded`**

```
PairCodeUpgraded(uint32 version);
```

Emitted when the pair code is updated

### **`RootCodeUpgraded`**

```
RootCodeUpgraded();
```

Emitted when the root code is updated

### **`ActiveUpdated`**

```
ActiveUpdated(bool new_active);
```

Emitted when the activity of dex root is updated

### **`RequestedPairUpgrade`**

```
RequestedPairUpgrade(address left_root, address right_root);
```

Emitted when the pair upgrade is requested

### **`RequestedForceAccountUpgrade`**

```
RequestedForceAccountUpgrade(address account_owner);
```

Emitted when forced account upgrade is requested

### **`RequestedOwnerTransfer`**

```
RequestedOwnerTransfer(address old_owner, address new_owner);
```

Emitted when transfer of ownership is requested

### **`OwnerTransferAccepted`**

```
OwnerTransferAccepted(address old_owner, address new_owner);
```

Emitted when transfer of ownership is accepted

### **`NewPairCreated`**

```
NewPairCreated(address left_root, address right_root);
```
Emitted when new pair is created
