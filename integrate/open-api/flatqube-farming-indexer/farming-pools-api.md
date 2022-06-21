# Farming pools API

{% swagger method="post" path="/farming_pools" baseUrl="http://farming.flatqube.io/v1" summary="Farming pools data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "pools_info": [
        {
            "pool_address": "0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0",
            "left_address": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
            "right_address": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
            "left_currency": "WEVER",
            "right_currency": "BRIDGE",
            "tvl": "17826322.032214433830",
            "tvl_change": "1.54",
            "apr": "59.7900",
            "apr_change": "-0.62",
            "share": "0",
            "user_token_balance": "0",
            "is_low_balance": false,
            "pool_owner_address": "0:a2b489a30c88648ab4bf98c2ba9d07c363c9d93e72a43a0625ff4644524582c6",
            "token_root_address": "0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2",
            "token_root_currency": "FLATQUBE-LP-WEVER-BRIDGE",
            "token_root_scale": 9,
            "farm_start_time": 1653004800000,
            "farm_end_time": null,
            "is_active": true,
            "reward_token_root_info": [
                {
                    "reward_root_address": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
                    "reward_currency": "BRIDGE",
                    "reward_scale": 9
                },
                {
                    "reward_root_address": "0:9f20666ce123602fd7a995508aeaa0ece4f92133503c0dfbd609b3239f3901e2",
                    "reward_currency": "QUBE",
                    "reward_scale": 9
                }
            ]
}
```
{% endswagger-response %}
{% endswagger %}

This method is used to display a list of all desired farming pools, for example to show a list of farming pools that the user marked as favorite. \
List is filtered by request body params such as left and right currencies and token addresses, farming pool root address, total value locked change, pool activity, etc.

### Request parameters

Body required. Data used for postman tests:

| Field name            | Example Value                                                                                                                          | Comment                                                                   |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| aprGe                 | 52.6300                                                                                                                                | value used for filtering all pools with APR greater than or equal to this |
| aprLe                 | 60                                                                                                                                     | value used for filtering all pools with APR less than or equal to this    |
| favoritePoolAddresses | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0                                                                     | address/addresses marked as favorite                                      |
| isActive              | true                                                                                                                                   | true if active pools should be retrieved, false if not                    |
| isAwaitingStart       | true                                                                                                                                   | true if the pools should be awaiting the start of farming, false if not   |
| isLowBalance          | false                                                                                                                                  | true if the balance should be low, false if not                           |
| isWithMyFarming       | true                                                                                                                                   | true if yes, false if no                                                  |
| leftAddress           | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d                                                                     | root address of the left currency                                         |
| leftCurrency          | WEVER                                                                                                                                  | symbol representing left currency                                         |
| limit                 | 0                                                                                                                                      | number of pools displayed per page                                        |
| offset                | 0                                                                                                                                      | offset                                                                    |
| rightAddress          | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1                                                                     | root address of the right currency                                        |
| rightCurrency         | BRIDGE                                                                                                                                 | symbol representing right currency                                        |
| rottAddress           | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1, 0:9f20666ce123602fd7a995508aeaa0ece4f92133503c0dfbd609b3239f3901e2 | lp address                                                                |
| tvlGe                 | 120177899                                                                                                                              | value used for filtering all pools with TVL greater than or equal to this |
| tvlLe                 | 12217899                                                                                                                               | value used for filtering all pools with TVL less than or equal to this    |
| userAddress           | 0:102cf118b6875d201a3011d5dc17a358ee4d4333ad7e167824515171ed8f6f63                                                                     | address of the user                                                       |

### Response field explanation

| Field name                | Example value                                                      | Comment                                                                   |
| ------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| Pools\_info               | -                                                                  | list of all available pools with following info                           |
| favorite\_pools\_info     | -                                                                  | list of all the farming pools user marked as favorite with following info |
| apr                       | 205                                                                | Annual Percentage Rate                                                    |
| apr\_change               | -0.50                                                              | APR change in the last 24h                                                |
| farm\_end\_time           | null                                                               | date time in UNIX format when does the farming in a certain pool end      |
| farm\_start\_time         | 1649289600000                                                      | date time in UNIX format when did the farming in a certain pool start     |
| is\_active                | true                                                               | true if the pool is active, false if not                                  |
| is\_low\_balance          | false                                                              | true if the balance is low, false if not                                  |
| left\_address             | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d | root address of the left currency in the pool                             |
| left\_currency            | WEVER                                                              | symbol of the left currency (ie. WEVER)                                   |
| pool\_address             | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | address of the current pool                                               |
| pool\_owner\_address      | 0:a2b489a30c88648ab4bf98c2ba9d07c363c9d93e72a43a0625ff4644524582c6 | address of the user that created the pool                                 |
| reward\_token\_root\_info | -                                                                  | list of reward tokens with following info about them                      |
| reward\_currency          | BRIDGE                                                             | symbol of the reward token                                                |
| reward\_root\_address     | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | root address of the certain reward token                                  |
| reward\_scale             | 9                                                                  | multiply reward amount with this value to get the right amount            |
| right\_address            | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | root address of the right currency in the pool                            |
| right\_currency           | BRIDGE                                                             | symbol of the right currency (ie. BRIDGE)                                 |
| share                     | 0                                                                  | amount of tokens user shared for contribution to the pool                 |
| token\_root\_address      | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2 | address of the liquidity pool                                             |
| token\_root\_currency     | FLATQUBE-LP-WEVER-BRIDGE                                           | name of the liquidity pool (ie. FLATQUBE-LP-WEVER-BRIDGE)                 |
| tvl                       | 17826322.032214433830                                              | total value locked (TVL) in that pool                                     |
| tvl\_change               | 1.54                                                               | TVL change in last 24h (percentage)                                       |
| user\_token\_balance      | 0                                                                  | balance of the user that is sharing his account on FlatQube               |
| favorite\_total\_count    | 4                                                                  | total number of user’s favorite farming pools                             |

### Example

```
app.post('/farming_pools', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/farming_pools`,
        data: {
            aprGe: req.body.aprGe,
            aprLe: req.body.aprLe,
            favoritePoolAddresses: req.body.favoritePoolAddresses,
            isActive: req.body.isActive,
            isAwaitingStart: req.body.isAwaitingStart,
            isLowBalance: req.body.isLowBalance,
            isWithMyFarming: req.body.isWithMyFarming,
            leftAddress: req.body.leftAddress,
            leftCurrency: req.body.leftCurrency,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            rightAddress: req.body.rightAddress,
            rightCurrency: req.body.rightCurrency,
            rootAddresses: req.body.rootAddresses,
            tvlGe: req.body.tvlGe,
            tvlLe: req.body.tvlLe,
            userAddress: req.body.userAddress,
            whiteCurrencyAddresses: req.body.whiteCurrencyAddresses,
            whiteListUri: req.body.whiteListUri
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

{% swagger method="post" path="/farming_pools/{farming_pool_address}" baseUrl="http://farming.flatqube.io/v1" summary="Farming pool data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

This method gets specific farming pool data by farming pool address.

It can be used for showing the desired farming pool with all the details about it, such as annual percentage rate, pool balance, right and left currencies and addresses, total value locked, etc.

### Request parameters

Farming\_pool\_address parameter required - represents address of a specific farming pool. \
Value used for testing is: `0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0`

Body required. Data used for postman tests:

| Field name       | Example value                                                      | Comment             |
| ---------------- | ------------------------------------------------------------------ | ------------------- |
| afterZeroBalance | true                                                               | -                   |
| userAddress      | 0:102cf118b6875d201a3011d5dc17a358ee4d4333ad7e167824515171ed8f6f63 | address of the user |

### Response field explanation

| Field name                | Example value                                                      | Comment                                                                      |
| ------------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| apr                       | 59.7                                                               | Annual Percentage Rate of the current pool                                   |
| apr\_change               | -0.62                                                              | APR change in the last 24h                                                   |
| farm\_end\_time           | null                                                               | date time in UNIX format when does the farming in a certain pool end         |
| farm\__start\_time_       | 1653004800000                                                      | date time in UNIX format when did the farming in a certain pool start        |
| history\_info             | -                                                                  | following info about user’s activity in this pool:                           |
| left\_amount              | 0                                                                  | amount of left currency reward                                               |
| right\_amount             | 0                                                                  | amount of right currency reward                                              |
| usdt\_amount              | 0                                                                  | total amount in USDT                                                         |
| is\_active                | true                                                               | true if the pool is active, false if not                                     |
| is\__low\_balance_        | false                                                              | true if the balance is low, false if not                                     |
| left\_address             | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d | root address of the left currency in the pool                                |
| left\_balance             | 41429655.89348116                                                  | total balance of the left currency in the pool                               |
| left\_currency            | WEVER                                                              | symbol of the left currency                                                  |
| pool\_address             | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | address of the current pool                                                  |
| pool\_balance             | 37424521.838044951                                                 | total balance of the LP tokens in the certain pool                           |
| pool\_info                | -                                                                  | contains following data regarding the certain pool:                          |
| rounds\_info              | -                                                                  | contains a list of farming rounds in the pool and following info about them: |
| end\_time                 | 1650412800                                                         | date time in UNIX format when did the round end                              |
| reward\_info              | -                                                                  | contains list of reward tokens along with additional info about the rewards: |
| rewardPerSec              | 0.0050                                                             | how many tokens are distributed as a reward per second                       |
| rewardTokenRootAddress    | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | symbol of the reward token                                                   |
| rewardTokenScale          | 9                                                                  | root address of the certain token                                            |
| start\_time               | 1650412800                                                         | date time in UNIX format when did the round start                            |
| vesting\_period           | 10368000                                                           | timeframe in which vesting will take place                                   |
| versting\_ratio           | 1000                                                               | percentage of remuneration that will be sent to vesting                      |
| pool\__owner\_address_    | 0:a2b489a30c88648ab4bf98c2ba9d07c363c9d93e72a43a0625ff4644524582c6 | address of the user that created the pool                                    |
| reward\_token\_root\_info | -                                                                  | list of reward tokens with following info about them:                        |
| reward\_currency          | BRIDGE                                                             | symbol of the reward token                                                   |
| reward\__per\_second_     | 0.0050                                                             | how many tokens are distributed as a reward per second                       |
| reward\__root\_address_   | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | root address of the certain reward token                                     |
| reward\__token\_scale_    | 9                                                                  | number used for scaling the reward amount                                    |
| right\_address            | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1 | root address of the right currency in the pool                               |
| right\_balance            | 815476.108391363066                                                | total balance of the left currency in the pool                               |
| right\_currency           | BRIDGE                                                             | symbol of the right currency                                                 |
| share                     | 0                                                                  | amount of tokens user shared for contribution to the pool                    |
| share\_change             | 0                                                                  | share change in percentage in the last 24h                                   |
| token\__root\_address_    | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2 | address of the liquidity pool                                                |
| token\__root\_scale_      | 9                                                                  | number used for scaling the lp token amount                                  |
| _token\_root\_currency_   | FLATQUBE-LP-WEVER-BRIDGE                                           | name of the liquidity pool                                                   |
| tvl                       | 17826322.032214433830                                              | total value locked (TVL) in that pool                                        |
| tvl\_change               | 1.54                                                               | TVL change in last 24h                                                       |
| user\__token\_balance_    | 0                                                                  | lp token balance of the user that is sharing his account on FlatQube         |
| user\__usdt\_balance_     | 0                                                                  | balance of the user that is sharing his account on FlatQube in USDT          |

### Example

```
 app.post('/farming_pools/:farming_pool_address', (req, res) => {
    console.log(`Request body data: ${req.params.farming_pool_address}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/farming_pools/${req.params.farming_pool_address}`,
        data: {
            afterZeroBalance: req.body.afterZeroBalance,
            userAddress: req.body.userAddress
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```
