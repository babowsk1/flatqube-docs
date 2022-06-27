---
description: Setting initial data when deploying new account or pair.
---

# DexPlatform

Smart contract used for setting initial data when deploying new account or pair.

### **`constructor`** 

```
constructor(TvmCell code, uint32 version, address vault, address send_gas_to) public
```

Initializes DexPlatform contract if the message sender is root or does the transfer to `send_gas_to` address. 

**Parameters:**

| Name        | Type     | Description                                                 |
|-------------|----------|-------------------------------------------------------------|
| code        | TvmCell  | Code to be set for this version                             |
| version     | uint32   | Current version of DexPlatform                              |
| vault       | address  | Vault address                                               |
| send_gas_to | address  | Address where to send gas spent by calling contract methods |

### **`_initialize`** 

```
function _initialize(TvmCell code, uint32 version, address vault, address send_gas_to) private
```

Initializes DexPlatform contract, stores parameters in TvmBuilder, sets current code and runs onCodeUpgrade from new code.

**Parameters:**

| Name        | Type     | Description                                                 |
|-------------|----------|-------------------------------------------------------------|
| code        | TvmCell  | Code to be set for this version                             |
| version     | uint32   | Current version of DexPlatform                              |
| vault       | address  | Vault address                                               |
| send_gas_to | address  | Address where to send gas spent by calling contract methods |

