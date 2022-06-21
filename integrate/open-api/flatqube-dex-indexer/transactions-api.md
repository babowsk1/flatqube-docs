# Transactions API

{% swagger method="post" path="/transactions" baseUrl="https://api.flatqube.io/v1" summary="Transactions data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "transactions": [
        {
            "messageHash": "beb4a1ba4cbf5d82bef26aee4020234100efe893d12d206a8b802a50cf0e19ed",
            "transactionHash": "a44818ac6ff16d485f65012ee1ff1faca9cf0182982f4e6aaf5fd0b706b45b2b",
            "left": "WBTC",
            "right": "BRIDGE",
            "tv": "47.866903714982",
            "leftValue": "120119",
            "rightValue": "5207609968",
            "userAddress": "0:41dc520061a68ba82de79c4748c3bfdb93bb7443203394890dad19905dbec8fd",
            "poolAddress": "0:ab39f6f37b9eb96f187199ff7f88745efe99bfa7624691f9f7d1e7713b6bc478",
            "leftAddress": "0:2ba32b75870d572e255809b7b423f30f36dd5dea075bd5f026863fceb81f2bcf",
            "rightAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
            "timestampBlock": 1649965345,
            "createdAt": 1649965352915,
            "eventType": "swaplefttoright",
            "fee": "0.00000361",
            "feeCurrency": "WBTC"
        },
...
}
```
{% endswagger-response %}
{% endswagger %}

This function needs to get Transactions data of a certain user filtered by required parameters.\
It can be used anywhere where a list of transactions should be shown and filtered using body parameters.

### Request parameters

Body required. Data used for Postman tests:

| Field name          | Example value                                                              | Comment                                                                                              |
| ------------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `createdAtGe`       | `0`                                                                        | Date time in UNIX format to filter all transaction that were created after or during that date time  |
| `createdAtLe`       | `0`                                                                        | Date time in UNIX format to filter all transaction that were created before or during that date time |
| `currencyAddress`   | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`       | Root address of the left currency in transaction pair                                                |
| `currencyAddresses` | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`       | Root address/addresses of a right currency in transaction pair                                       |
| `eventType`         | `swaplefttoright`                                                          | Type of the transaction (swap, add, remove)                                                          |
| `leftAmountGe`      | `0.194319663088308553962886430`                                            | Amounts that are greater or equal to the given value of the left transaction pair                    |
| `leftAmountLe`      | `9.029870729776`                                                           | Amounts that are less or equal to the given value of the left transaction pair                       |
| `limit`             | `0`                                                                        | Amount limitation                                                                                    |
| `offset`            | `0`                                                                        |                                                                                                      |
| `ordering`          | `blocktimeascending`                                                       | Order transactions by time ascending or descending                                                   |
| `poolAddress`       | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06`       | Address of the pair’s pool                                                                           |
| `rightAmountGe`     | `7.029870729776`                                                           | Amounts that are greater or equal to the given value of the right transaction pair                   |
| `rightAmountLe`     | `9.029870729776`                                                           | Amounts that are less or equal to the given value of the right transaction pair                      |
| `timestampBlockGe`  | `0`                                                                        | Filter timestamp of the blocks that are greater or equal to this value                               |
| `timestampBlockLe`  | `0`                                                                        | Filter timestamp of the blocks that are less or equal to this value                                  |
| `tvGe`              | `8955040.156573434959`                                                     | Filter transactions with total value greater than or equal to this value                             |
| `tvLe`              | `8955043.156573434959`                                                     | Filter transactions with total value less than or equal to this value                                |
| `userAddress`       | `0:3aeefed73a08979d5f7d489e7fe06f0d20a433e27f81b70a4e2e0d7f3968ede8`       | Address of the user initiating transactions                                                          |
| `whiteListUri`      | `https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json` | Path to a white list                                                                                 |

### Response explanation

| Field name        | Example value                                                        | Comment                                           |
| ----------------- | -------------------------------------------------------------------- | ------------------------------------------------- |
| `count`           | 10                                                                   | Amount of transactions shown per page             |
| `offset`          | 0                                                                    |                                                   |
| `totalCount`      | 4132                                                                 | Number of all transactions required               |
| `transactions`    | -                                                                    | Date time in UNIX format of transaction formation |
| `createdAt`       | `1649965461706`                                                      | Date time in UNIX format of transaction formation |
| `eventType`       | `deposit`                                                            | Type of transaction (swap, add, remove)           |
| `fee`             | `null`                                                               | Transaction fee                                   |
| `feeCurrency`     | `null`                                                               | Currency of the transaction fee                   |
| `left`            | `WEVER`                                                              | Left pair currency                                |
| `leftAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | Left pair root address                            |
| `leftValue`       | `915417342444`                                                       | Left pair value                                   |
| `messageHash`     | `c264d77bf677742d3d0c8065b92d1bf6137444917e20fafebe9a6b7f3376bd24`   | Hash code of the transaction message              |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | Address of the pair’s pool                        |
| `right`           | `BRIDGE`                                                             | Right pair currency                               |
| `rightAddress`    | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | Right pair root address                           |
| `rightValue`      | `22933551212`                                                        | Right pair value                                  |
| `timestampBlock`  | `1649965452`                                                         | Date time of block formation                      |
| `transactionHash` | `49bf48242de460facac859896ad9987d065d8bb15395f14ca907020cff32aba9`   | Hash of the transaction                           |
| `tv`              | `421.597659752853`                                                   | Total value in transaction (in USD)               |
| `userAddress`     | `0:b2475c0716d754fba88eb28e12b45e6f636729f96270aebb859730af86182cf4` | Address of the user that created the transaction  |

### Example

```
 app.post('/transactions', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/transactions`,
        data: {
            createdAtGe: req.body.createdAtGe,
            createdAtLe: req.body.createdAtLe,
            currencyAddress: req.body.currencyAddress,
            currencyAddresses: req.body.currencyAddresses,
            eventType: req.body.eventType,
            leftAmountGe: req.body.leftAmountGe,
            leftAmountLe: req.body.leftAmountLe,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            poolAddress: req.body.poolAddress,
            rightAmountGe: req.body.rightAmountGe,
            rightAmountLe: req.body.rightAmountLe,
            timestampBlockGe: req.body.timestampBlockGe,
            timestampBlockLe: req.body.timestampBlockLe,
            tvGe: req.body.tvGe,
            tvLe: req.body.tvLe,
            userAddress: req.body.userAddress,
            whiteListUri: req.body.whiteListUri,
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error') }) })
```
