# Pairs API

{% swagger method="post" path="/pairs" baseUrl="https://api.flatqube.io/v1" summary="Pairs data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
 ...
"counter": "BRIDGE",
        "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
        "fee": "0.3000"
      },
      "tvl": "8955040.156573434959",
      "tvlChange": "3.26",
      "leftLocked": "22564291945792668",
      "leftPrice": "0.2323725625631798673951181204",
...
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get all Pairs data by\
\
It can be used for representing data specific to each currency in detail.

### Request parameters

Body required. Data used for Postman tests:

| Field name          | Example value                                                              | Comment                                     |
| ------------------- | -------------------------------------------------------------------------- | ------------------------------------------- |
| `currencyAddress`   | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`       | `address of the currency for the left pair` |
| `currencyAddresses` | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`       | `list of addresses`                         |
| `limit`             | `0`                                                                        | `number of pairs that should be retrieved`  |
| `offset`            | `0`                                                                        |                                             |
| `ordering`          | `tvlascending`                                                             | `order by pair’s TVL ascending/descending`  |
| `tvlAmountGe`       | `8955040.156573434959`                                                     | `highest TVL amount`                        |
| `tvlAmountLe`       | `8955043.156573434959`                                                     | `lowest TVL amount`                         |
| `whiteListUri`      | `https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json` | `path to a white list`                      |

```
{
  "currencyAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
  "currencyAddresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ],
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "tvlAmountGe": "8955040.156573434959",
  "tvlAmountLe": "8955043.156573434959",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```

### Response fields explanation

| Field name        | Example value                                                        | Comment                                                |
| ----------------- | -------------------------------------------------------------------- | ------------------------------------------------------ |
| `count`           | `0`                                                                  | number of pairs displayed on one page                  |
| `offset`          | `0`                                                                  |                                                        |
| `pairs`           |                                                                      | list of pairs with following info:                     |
| `fee24h`          | `184.89949`                                                          | total amount of fees (in USD) in the last 24h          |
| `fee7d`           | `1531.12412`                                                         | total amount of fees (in USD) in the last 7 days       |
| `feeAllTime`      | `5886.2023`                                                          | total amount of fees (in USD) EVER                     |
| `leftLocked`      | `22564291945792668`                                                  | tvl of the left pair (token) in USD                    |
| `leftPrice`       | `0.234234123`                                                        | price (in USD) of the left pair                        |
| `meta`            |                                                                      | object containing following data:                      |
| `base`            | `WEVER`                                                              | left token name (ie. WEVER)                            |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | root address of the left token                         |
| `counter`         | `BRIDGE`                                                             | right token name (ie. BRIDGE)                          |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | root address of the right token                        |
| `fee`             | `0.300`                                                              | fees for trading between left and right token          |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | address of the pool of left and right pair             |
| `rightLocked`     | `565424319668420`                                                    | tvl of the right pair (token) in USD                   |
| `rightPrice`      | `9.306709686682`                                                     | price (in USD) of the left pair                        |
| `tvl`             | `8955040.156573434959`                                               | TVL in the pair’s pool                                 |
| `tvlChange`       | `3.26`                                                               | TVL change (percentage) in the pool for the last 24h   |
| `volume24h`       | `61614.202233211332`                                                 | trading volume of the pair in the last 24h (in USD)    |
| `volume7d`        | `563110.817462570605`                                                | trading volume of the pair in the last 7 days (in USD) |
| `volumeChange24h` | `85.03`                                                              | trading volume change (percentage) in the last 24h     |
| `totalCount`      | `1`                                                                  | total number of pairs that satisfies search parameters |

### Example

```
app.post('/pairs', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs`,
        data: {
            currencyAddress: req.body.currencyAddress,
            currency_addresses: req.body.currency_addresses,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            tvlAmountGe: req.body.tvlAmountGe,
            tvlAmountLe: req.body.tvlAmountLe,
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

{% swagger method="post" path="/pairs/address/{address}" baseUrl="https://api.flatqube.io/v1" summary="Dex pair data info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "meta": {
    "base": "WEVER",
    "baseAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
    "counterAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
    "counter": "BRIDGE",
    "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
    "fee": "0.3000"
  },
  "tvl": "11991318.532110678860",
  "tvlChange": "1.58",
  "leftLocked": "25793313867480582",
  "leftPrice": "0.2324501340486766469128429809",
  "rightLocked": "644828780315691",
  "rightPrice": "9.298063996337",
  "volume24h": "71793.071260381244",
  "volumeChange24h": "-40.15",
  "volume7d": "1568911.947379165588",
  "fee24h": "215.553088264148",
  "fee7d": "4697.356377562167",
  "feeAllTime": "18787.266129440217"
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get pair data info by liquidity pool address.

It can be used for presenting a pair with all the details about it in the desired pool.

### Request parameters

Address parameter required - represents the pool address of a specific pair.\
_Value used for testing is pool WEVER/BRIDGE address: `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06`_

### Response field explanation

| Field name        | Example value                                                        | Comment                                                |
| ----------------- | -------------------------------------------------------------------- | ------------------------------------------------------ |
| `meta`            | _\`\`_                                                               | object containing the following data:                  |
| `base`            | _`WEVER`_                                                            | left token name (ie. WEVER)                            |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | root address of the left token                         |
| `counter`         | `BRIDGE`                                                             | right token name (ie. BRIDGE)                          |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | root address of the right token                        |
| `fee`             | `0.3000`                                                             | fees for trading between left and right token          |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | address of the pool containing left and right pair     |
| `tvl`             | `11992480.952892429456`                                              | TVL in the pair’s pool                                 |
| `tvlChange`       | `1.22`                                                               | TVL change (percentage) in the pool for the last 24h   |
| `leftLocked`      | `25795814233390122`                                                  | TVL of the left pair (token) in USD                    |
| `leftPrice`       | `0.2324501340486766469128429809`                                     | price (in USD) of the left pair                        |
| `rightLocked`     | `644766509092723`                                                    | TVL of the right pair (token) in USD                   |
| `rightPrice`      | `9.299863426349`                                                     | price (in USD) of the left pair                        |
| `volume24h`       | `68293.598448021590`                                                 | trading volume of the pair in the last 24h (in USD)    |
| `volumeChange24h` | `-44.98`                                                             | trading volume change (percentage) in the last 24h     |
| `volume7d`        | `1549070.057378500757`                                               | trading volume of the pair in the last 7 days (in USD) |
| `fee24h`          | `205.053510628491`                                                   | total amount of fees (in USD) in the last 24h          |
| `fee7d`           | `4637.831319664494`                                                  | total amount of fees (in USD) in the last 7 days       |
| `feeAllTime`      | `18789.418763913485`                                                 | total amount of fees (in USD) EVER                     |

### Example

```
 app.post('/pairs/address/:address', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/address/${req.params.address}`
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

{% swagger method="post" path="/pairs/cross_pairs" baseUrl="https://api.flatqube.io/v1" summary="Dex cross pairs data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "meta": {
    "base": "WEVER",
    "baseAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
    "counterAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
    "counter": "BRIDGE",
    "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
    "fee": "0.3000"
  },
  "tvl": "11992480.952892429456",
  "tvlChange": "1.22",
  "leftLocked": "25795814233390122",
  "leftPrice": "0.2324501340486766469128429809",
  "rightLocked": "644766509092723",
  "rightPrice": "9.299863426349",
  "volume24h": "68293.598448021590",
  "volumeChange24h": "-44.98",
  "volume7d": "1549070.057378500757",
  "fee24h": "205.053510628491",
  "fee7d": "4637.831319664494",
  "feeAllTime": "18789.418763913485"
}
```
{% endswagger-response %}
{% endswagger %}

This function is needs to get all cross pairs data.

It can be used anywhere where certain details about one currency and how it affects the other one in the pair and vice versa is needed.

### Request parameters

Body required. Data used for Postman tests:

| Field name            | Example value                                                        | Comment                                                                                                        |
| --------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `fromCurrencyAddress` | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | currency address for which to retrieve cross pairs                                                             |
| `toCurrencyAddresses` | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | currency address/addresses we are checking weather it is a pair with currency in fromCurrencyAddress parameter |

### Response fields explanation:

| Field name        | Example value                                                        | Comment                                                                      |
| ----------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `pairs`           |                                                                      | a list of pairs based on the given addresses including details of the pairs: |
| `meta`            |                                                                      | object containing following data:                                            |
| `base`            | `WEVER`                                                              | left token name (ie. WEVER)                                                  |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | root address of the left token                                               |
| `counter`         | `BRIDGE`                                                             | right token name (ie. BRIDGE)                                                |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | root address of the right token                                              |
| `fee`             | `0.300`                                                              | fees for trading between left and right token                                |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | address of the pool containing left and right pair                           |
| `tvl`             | `11992480.952892429456`                                              | TVL in the pair’s pool                                                       |
| `tvlchange`       | `1.22`                                                               | TVL change (percentage) in the pool for the last 24h                         |
| `leftLocked`      | `25795814.233390122000`                                              | TVL of the left pair (token) in USD                                          |
| `leftPrice`       | `0.2322839661557624874057319495`                                     | price (in USD) of the left pair                                              |
| `rightLocked`     | `644766.509092723000`                                                | TVL of the right pair (token) in USD                                         |
| `rightPrice`      | `9.293215382388`                                                     | price (in USD) of the right pair                                             |
| `volume24h`       | 68293.598448021590                                                   | trading volume of the pair in the last 24h (in USD)                          |
| `volume7d`        | `1549070.057378500757`                                               | trading volume of the pair in the last 7 days (in USD)                       |
| `volumechange24h` | `-44.98`                                                             | trading volume change (percentage) in the last 24h                           |
| `fee24h`          | `205.053510628491`                                                   | total amount of fees (in USD) in the last 24h                                |
| `fee7d`           | `4637.831319664494`                                                  | total amount of fees (in USD) in the last 7 days                             |
| `feeAllTime`      | `18789.418763913485`                                                 | total amount of fees (in USD) EVER                                           |
| `offset`          | `0`                                                                  |                                                                              |
| `count`           | `10`                                                                 | number of pairs to display per page                                          |
| `totalCount`      | `1`                                                                  | total number of pairs retrieved                                              |

### Example

```
app.post('/pairs/cross_pairs', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/cross_pairs`,
        data: {
            fromCurrencyAddress: req.body.fromCurrencyAddress,
            toCurrencyAddresses: req.body.toCurrencyAddresses
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

{% swagger method="post" path="/pairs/left/{left}/right/{right}" baseUrl="https://api.flatqube.io/v1" summary="Pair data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "meta": {
    "base": "WEVER",
    "baseAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
    "counterAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
    "counter": "BRIDGE",
    "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
    "fee": "0.3000"
  },
  "tvl": "11992480.952892429456",
  "tvlChange": "1.22",
  "leftLocked": "25795814233390122",
  "leftPrice": "0.2322691452075765631601791831",
  "rightLocked": "644766509092723",
  "rightPrice": "9.292622425991",
  "volume24h": "68293.598448021590",
  "volumeChange24h": "-44.98",
  "volume7d": "1549070.057378500757",
  "fee24h": "205.053510628491",
  "fee7d": "4637.831319664494",
  "feeAllTime": "18789.418763913485"
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get pair data info by token root addresses. It can be used anywhere where details about the pairs are used and should be retrieved using their root addresses.

### Request parameters

Left and right parameter required - represents address of a specific currency.\
Value used for testing are WEVER and BRIDGE addresses (respectively) :\
left = `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`\
\`\`right = `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`

### Response field explanation:

| Field name        | Example value                                                        | Comment                                                                      |
| ----------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `pairs`           |                                                                      | a list of pairs based on the given addresses including details of the pairs: |
| `meta`            |                                                                      | object containing following data:                                            |
| `base`            | `WEVER`                                                              | left token name (ie. WEVER)                                                  |
| `baseAddress`     | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | root address of the left token                                               |
| `counter`         | `BRIDGE`                                                             | right token name (ie. BRIDGE)                                                |
| `counterAddress`  | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1` | root address of the right token                                              |
| `fee`             | `0.300`                                                              | fees for trading between left and right token                                |
| `poolAddress`     | `0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06` | address of the pool containing left and right pair                           |
| `tvl`             | `11992480.952892429456`                                              | TVL in the pair’s pool                                                       |
| `tvlchange`       | `1.22`                                                               | TVL change (percentage) in the pool for the last 24h                         |
| `leftLocked`      | `25795814.233390122000`                                              | TVL of the left pair (token) in USD                                          |
| `leftPrice`       | `0.2322839661557624874057319495`                                     | price (in USD) of the left pair                                              |
| `rightLocked`     | `644766.509092723000`                                                | TVL of the right pair (token) in USD                                         |
| `rightPrice`      | `9.293215382388`                                                     | price (in USD) of the right pair                                             |
| `volume24h`       | 68293.598448021590                                                   | trading volume of the pair in the last 24h (in USD)                          |
| `volume7d`        | `1549070.057378500757`                                               | trading volume of the pair in the last 7 days (in USD)                       |
| `volumechange24h` | `-44.98`                                                             | trading volume change (percentage) in the last 24h                           |
| `fee24h`          | `205.053510628491`                                                   | total amount of fees (in USD) in the last 24h                                |
| `fee7d`           | `4637.831319664494`                                                  | total amount of fees (in USD) in the last 7 days                             |
| `feeAllTime`      | `18789.418763913485`                                                 | total amount of fees (in USD) EVER                                           |

### Example

```
app.post('/pairs/left/:left/right/:right', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/left/${req.params.left}/right/${req.params.right}`
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

{% swagger method="post" path="/pairs/left/{left}/right/{right}/ohlcv" baseUrl="https://api.flatqube.io/v1" summary="Ohlcv Pair data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
 {
    "open": "0.024984390565",
    "high": "0.025131270323",
    "low": "0.024980850704",
    "close": "0.025131270323",
    "volume": "249.621417263132",
    "openTimestamp": 1647274428000,
    "closeTimestamp": 1647275606000,
    "timestamp": 1647273600000
  },
  ...
  }
```
{% endswagger-response %}
{% endswagger %}

This function needs to get ohlcv pair data info by token root addresses.\
\
It can be used ie. for graphic representation of price change of the right pair compared to the value of the left pair over a certain period of time (ie. 1 WEVER = 0.02245627 BRIDGE).

### Request parameters

Left parameter required - represents the address of a specific currency.\
Value used for testing is WEVER address: `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d`

Right parameter required - represents the address of a specific currency.\
Value used for testing is BRIDGE address:\
`0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`

Data used for Postman tests:

| Field name  | Example value   | Comment                                                                                                           |
| ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------- |
| `from`      | `1646741858511` | Date time in UNIX format for the start of timeframe (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time) |
| `timeframe` | `H1`            | desired timeframe to retrieve prices data, could be set for hours, days, etc. (“H1”, “D1”...)                     |
| `to`        | `1647346658513` | date time in UNIX format for the end of timeframe (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)           |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### Response field explanation

| Field name       | Example value      | Comment                                                                                                                                                                        |
| ---------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `close`          | `0.025131270323`   | Value of the currency (in USD) in the last moment of given timeframe                                                                                                           |
| `closeTimestamp` | `1647275606000`    | Date time for the “close” value in UNIX format                                                                                                                                 |
| `high`           | `0.025131270323`   | The highest currency price in the given timeframe                                                                                                                              |
| `low`            | `0.024980850704`   | The lowest currency price in the given timeframe                                                                                                                               |
| `open`           | `0.024984390565`   | Value of the currency (in USD) in the first moment of the given timeframe                                                                                                      |
| `openTimestamp`  | `1647274428000`    | Date time for the “open” value in UNIX format                                                                                                                                  |
| `timeStamp`      | `1647273600000`    | date time in UNIX format, the round value of openTimestamp (ex. openTimeStamp is March 8, 2022 11:25:48 PM, timeStamp will be March 8, 2022 11:00:00 PM when converted to GMT) |
| `volume`         | `249.621417263132` | Trading volume (in USD) for the given currency between openTimeStamp and closeTimeStamp)                                                                                       |

### Example

```
 app.post('/pairs/left/:left/right/:right/ohlcv', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/left/${req.params.left}/right/${req.params.right}/ohlcv`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
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
