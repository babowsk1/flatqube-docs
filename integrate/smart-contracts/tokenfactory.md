---
discription: The TokenFactory smart contract is used for deploying tokens, sets wallet, root, platform codes and managing ownership.
---

# TokenFactory

Smart contract responsible for deploying tokens, sets wallet, root, platform codes and managing ownership.

Derives following classes and interfaces: *ITokenFactory, IUpgradable*.

### **`constructor`**

```
constructor(address _owner) public
```

Parameters:

| Name   | Type    | Description                        |
|--------|---------|------------------------------------|
| _owner | address | Address of the token factory owner |

## Token

### **`createToken`** 

```
function createToken(uint32 callId, string name, string symbol, uint8 decimals, address initialSupplyTo, uint128 initialSupply, uint128 deployWalletValue, bool mintDisabled, bool burnByRootDisabled, bool burnPaused, address remainingGasTo) public override
```

Fills the token data taken from function params, creates token root address calling `TokenRootUpgradable`, emits `TokenCreated` event and `onTokenRootDeployed` callback.

Parameters:

| Name               | Type    | Description                                                    |
|--------------------|---------|----------------------------------------------------------------|
| callId             | uint32  | ID of the operation call                                       |
| name               | string  | Token name                                                     |
| symbol             | string  | Token symbol                                                   |
| decimals           | uint8   | Number of decimals                                             |
| initialSupplyTo    | address | Address which will hold initial supply of newly created token  |
| initialSupply      | uint128 | Number of tokens initially available                           |
| deployWalletValue  | uint128 | Value necessary for deploying new token’s wallet               |
| mintDisabled       | bool    | True if minting is disabled, false if not                      |
| burnByRootDisabled | bool    | True if burn is disabled, false if not                         |
| burnPaused         | bool    | True if burn is paused, false if not                           |
| remainingGasTo     | address | Address where to store remaining gas after creating token root |

## Owner

### **`transferOwner`** 

```
function transferOwner(address newOwner) external responsible onlyOwner returns(address)
```

Takes new owner address, delegate it to the `pendingOwner` and returns `pendingOwner` (new owner address).

Parameters:

| Name     | Type    | Description            |
|----------|---------|------------------------|
| newOwner | address | Address of a new owner |

Return Value:

| Type    | Description             |
|---------|-------------------------|
| address | Pending owner’s address |

### **`acceptOwner`** 

```
function acceptOwner() external responsible returns(address)
```

If sender is pending owner, owner takes `pendingOwner` address and returns it, meaning the new owner is accepted.

Return Value:

| Type    | Description              |
|---------|--------------------------|
| address | Address of the new owner |

## Code

### **`setRootCode`**

```
function setRootCode(TvmCell _rootCode) public onlyOwner
```

Takes `_rootCode` from function params, delegates it to `rootCode` and returns it.

Parameters:

| Name      | Type    | Description          |
|-----------|---------|----------------------|
| _rootCode | TvmCell | New token root code  |

### **`setWalletCode`** 

```
function setWalletCode(TvmCell _walletCode) public onlyOwner
```

Same as root. 

Parameters:

| Name        | Type    | Description     |
|-------------|---------|-----------------|
| _walletCode | TvmCell | New wallet code |

### **`setWalletPlatformCode`** 

```
function setWalletPlatformCode(TvmCell _walletPlatformCode) public onlyOwner
```

Same as root.

Parameters:

| Name                | Type    | Description                  |
|---------------------|---------|------------------------------|
| _walletPlatformCode | TvmCell | New platform code for wallet |

## Upgrade

### **`upgrade`** 

```
function upgrade(TvmCell code) public override onlyOwner
```

upgrades token to a new version with a new code taken from params. 

Parameters:

| Name | Type    | Description                               |
|------|---------|-------------------------------------------|
| code | TvmCell | New version code used for upgrading token |

## Key Events

### **`TokenCreated`**

```
TokenCreated(address tokenRoot);
```