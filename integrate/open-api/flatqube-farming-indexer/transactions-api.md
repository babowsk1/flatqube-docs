# Transactions API

{% swagger method="post" path="/transactions" baseUrl="http://farming.flatqube.io/v1" summary="Transactions data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "transactions": [
        {
            "messageHash": "254f05f87ae6d283ce7fc3bcb13919e0a35b2781db54e50046bde369d9a47f2d",
            "transactionHash": "760aa87b1fd7bcbbccae87ab52b187238ac91638f132b048380f711f55e17d4a",
            "kind": "Withdraw",
            "userAddress": "0:f1f1158fcf4f0725a5a53c4d1ac1d37583b36eb4e9ab542d3a288424f6762fdd",
            "poolAddress": "0:f96da52e928cf4d8e54dcec0e7f7fefddfb7592590f05705dcaa9f211102fbc5",
            "tokenAddress": "0:0bf177d4dcc468293502ce81fd9a05285f7621814a705a000020dc15fa8258f8",
            "tokenCurrency": "FLATQUBE-LP-QUBE-WEVER",
            "tokenExec": "9926.264109806000",
            "tvExec": "11289.535028128434",
            "leftExec": "117.580203251916",
            "rightExec": "17702.052927191519",
            "timestampBlock": 1650533932000
        }
    ],
    "totalCount": 1
}
```
{% endswagger-response %}
{% endswagger %}

This method gets transaction data.

It can be used for showing a list of all desired transactions filtered by request body params such as transaction type, user address, pool address, etc. \
For example, showing detailed information of all the withdrawal transactions of the specific user.

### Required data

Body required. Data used for postman tests:

| Field name             | Example value                                                                                                                                        | Comment                                                                                                  |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| eventTypes             | deposit                                                                                                                                              | type of transaction (deposit, withdraw…)                                                                 |
| limit                  | 10                                                                                                                                                   | maximum number of transactions that should be returned                                                   |
| poolAddress            | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0                                                                                   | address of the farming pool in which transactions are being processed                                    |
| rootAddress            | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2                                                                                   | address of the LP token                                                                                  |
| rootTokenAmountGe      | 12400                                                                                                                                                | value used for filtering all transactions with lp token amount greater than or equal to this             |
| rootTokenAmountLe      | 12600                                                                                                                                                | value used for filtering all transactions with lp token amount less than or equal to this                |
| timestampBlockGe       | 1647590400000                                                                                                                                        | date time used for filtering all transactions with block timestamp greater than or equal to this         |
| timestampBlockLe       | 1648195200000                                                                                                                                        | date time used for filtering all transactions with block timestamp less than or equal to this            |
| tvGe                   | 5800                                                                                                                                                 | value used for filtering all transactions with total value amount (in USD) greater than or equal to this |
| tvLe                   | 6500                                                                                                                                                 | value used for filtering all transactions with total value amount (in USD) less than or equal to this    |
| userAddress            | 0:0e7ebac7bdfcec9edb511113774c75e8c4949d2c5ab2b903837bd2ff04128d68                                                                                   | address of the user                                                                                      |
| whiteCurrencyAddresses | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d, 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1               | -                                                                                                        |
| whiteListUri           | [https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json](https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json) | path to the whitelist                                                                                    |

### Response field explanation

| Field name      | Example value                                                      | Comment                                                         |
| --------------- | ------------------------------------------------------------------ | --------------------------------------------------------------- |
| totalCount      | 2                                                                  | total transactions number in one pool                           |
| Transactions    | -                                                                  | list of all the transactions containing following data          |
| kind            | Withdraw                                                           | what kind of transaction (Deposit, Claim, Withdraw…)            |
| leftExec        | null                                                               | amount of left currency participating in the transaction        |
| messegeHash     | 80056a0cb8ea3a2710edd823b9250d8ee717c825079c50667d4c84824138f2d6   | hash of the transaction message                                 |
| poolAddress     | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | address of the pool                                             |
| rightExec       | 148.559845816278                                                   | amount of right currency participating in the transaction       |
| timestampBlock  | 1649355777000                                                      | date time in UNIX format when the transaction block was created |
| tokenAddress    | 0:5c66f770d439212181bb6f62714bc235f754653ad9e2aca5a685ff7979174ea2 |  LP token address                                               |
| tokenCurrency   | FLATQUBE-LP-WEVER-BRIDGE                                           |  LP token symbol                                                |
| tokenExec       | 6333.372380447000                                                  | token amount in the transaction                                 |
| transactionHash | b78457c3ca523321bed353567954ded6cd8af94dfff32aae7098f33cd9603bfa   | hash code of the transaction                                    |
| tvExec          | 2719.899465109213                                                  | total amount (in USD) in the transaction                        |
| userAddress     | 0:f1f1158fcf4f0725a5a53c4d1ac1d37583b36eb4e9ab542d3a288424f6762fdd | address of the user initiating the transaction                  |

### Example

```
 app.post('/transactions', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/transactions`,
        data: {
            eventTypes: req.body.eventTypes,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            poolAddress: req.body.poolAddress,
            rootAddresses: req.body.rootAddresses,
            rootTokenAmountGe: req.body.rootTokenAmountGe,
            rootTokenAmountLe: req.body.rootTokenAmountLe,
            timestampBlockGe: req.body.timestampBlockGe,
            timestampBlockLe: req.body.timestampBlockLe,
            tvGe: req.body.tvGe,
            tvLe: req.body.tvLe,
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
