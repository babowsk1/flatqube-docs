# Currencies API

{% swagger method="post" path="/{currencies}" baseUrl="https://api.flatqube.io/v1/currencies" summary="Currency data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Request succesfull" %}
```
{
  "currency": "WEVER",
  "address": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
  "price": "0.2282687283977780064244925674",
  "priceChange": "-3.71",
  "tvl": "12209750.651450054502",
  "tvlChange": "-2.45",
  "volume24h": "555590.207631653593",
  "volumeChange24h": "22.66",
  "volume7d": "3700214.440186123499",
  "fee24h": "1660.849630640965",
  "transactionsCount24h": 768
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get currency data info by token root address.\
\
It can be used for representing data specific to each currency in detail.

### Request parameters

_Currencies parameter required - represents address of a specific currency._

_Value used for testing is WEVER address: 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d_

### Response fields explanation <a href="#response-fields-explanation" id="response-fields-explanation"></a>

| Field name        | Example value                                                        | Comment                                                  |
| ----------------- | -------------------------------------------------------------------- | -------------------------------------------------------- |
| `currency`        | `WEVER`                                                              | currency symbol                                          |
| `address`         | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | root address of the desired currency price: price in USD |
| `priceChange`     | `-3.71`                                                              | price change in the last 24h (percentage)                |
| `tvl`             | `12209750.651450054`                                                 | total value locked (TVL in USD) of the currency          |
| `tvlChange`       | `-2.45`                                                              | TVL change in the last 24h (percentage)                  |
| `volume24h`       | `555590.207631653593`                                                | trading volume (in USD) in the last 24h                  |
| `volumeChange24h` | `22.66`                                                              | trading volume change (percentage) in the last 24h       |
| `volume7d`        | `3700214.4401861234`                                                 | trading volume (in USD) in the last 7 days               |

### Example

```java
app.post('/currencies/:currencies', (req, res) => {
        console.log(`Method params: ${req.params.currencies}`)
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/currencies/${req.params.currencies}`
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

{% swagger method="post" path="" baseUrl="https://api.flatqube.io/v1/currencies" summary="DEX currency USD price" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
  "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1": "9.892687544928"
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get currency prices in USD by token root address/addresses.\
\
It can be used anywhere where a conversion value of a certain currency should be shown in USDT.

### Request parameters

_Body required. Data used for Postman tests:_

```
{
  "currency_addresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"  ]
}
```

### Example

```
app.post('/currencies_usdt_prices', (req, res) => {
        console.log(`Request body data: ${req.body.currency_addresses}`)
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/currencies_usdt_prices`,
            data: {
                currency_addresses: req.body.currency_addresses
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

{% swagger method="post" path="/currencies" baseUrl="https://api.flatqube.io/v1" summary="DEX all currencies info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```javascript
```
{% endswagger-response %}
{% endswagger %}

This function gets currency data info.\
It retrieves all desired currencies based on their addresses and other requested body parameters.\
\
It can be used to show all currencies and their data in a list format.

### Request parameters

_Body required._ Data used for Postman tests:

```
  {
  "currency_addresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ],
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```

### Response fields explanation

| Field name             | Example value                                                        | Comment                                                    |
| ---------------------- | -------------------------------------------------------------------- | ---------------------------------------------------------- |
| `count`                |                                                                      | number of currencies per page                              |
| `currencies`           |                                                                      | list of all retrieved currencies with the following data:  |
| `address`              | `0:b5ff077d8ac0160559bd3c945a2a824cda12ba93ae90c2697c890656d52fc7d0` | root address of the currency                               |
| `currency`             | `MOON`                                                               | symbol of the currency                                     |
| `fee24h`               | `2.107170214758`                                                     | currency fees in the last 24h price: currency price in USD |
| `priceChange`          | `-14.52`                                                             | price change in the last 24h (percentage)                  |
| `transactionsCount24h` | `18`                                                                 | number of the transactions in the last 24h                 |
| `tvl`                  | `6304.683075841390`                                                  | TVL (total value locked) amount (in USD)                   |
| `tvlChange`            | `-8.12`                                                              | TVL change (percentage) in the last 24h                    |
| `volume24h`            | `713.328162545779`                                                   | trading volume amount (in USD) in the last 24h             |
| `volume7d`             | `15925.850567579295`                                                 | trading volume amount (in USD) in the last 7 days          |
| `volumeChange24h`      | `-34.83`                                                             | trading volume change (percentage) in the last 24h         |
| `offset`               |                                                                      | offset                                                     |
| `totalCount`           | `19`                                                                 | number of all the currencies retrieved                     |

### Example

```
app.post('/currencies', (req, res) => {
    console.log(`Request body data: ${req.body.currency_addresses}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies`,
        data: {
            currency_addresses: req.body.currency_addresses,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
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

{% swagger method="post" path="/{currencies}/prices" baseUrl="https://api.flatqube.io/v1/currencies" summary="DEX currency price info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
[
  {
    "open": "0.997085448681",
    "high": "0.997085448681",
    "low": "0.997085448681",
    "close": "0.997085448681",
    "volume": "0",
    "openTimestamp": 1646740800000,
    "closeTimestamp": 1646744400000,
    "timestamp": 1646740800000
  },
  ...
  ]
```
{% endswagger-response %}
{% endswagger %}

This function gets currency price data info based on the timespan given.\
\
It can be used for graphic representation of price change over a certain period of time.

### Request parameters

Currencies parameter required - represents address of a specific currency.

Value used for testing is Dai Stablecoin address: 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9

Body required. Example data used for Postman tests:

| Field name  | Example value                                               | Comment                                                                       |
| ----------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `from`      | `1646741858511` or `March 8, 2022 12:17:38.511 PM GMT time` | Date-time in UNIX format for the start of timeframe                           |
| `timeframe` | `“H1”, “D1”`                                                | Desired timeframe to retrieve prices data, could be set for hours, days, etc. |
| `to`        | `1647346658513` or `March 15, 2022 12:17:38.513 PM`         | Date-time in UNIX format for the end of timeframe                             |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### Response fields explanation

| Field name       | Example value    | Comment                                                    |
| ---------------- | ---------------- | ---------------------------------------------------------- |
| `close`          | `0.997085448681` | number of currencies per page                              |
| `closeTimestamp` | `1646744400000`  | list of all retrieved currencies with the following data:  |
| `high`           | `0.997085448681` | root address of the currency                               |
| `low`            | `0.997085448681` | symbol of the currency                                     |
| `openTimestamp`  | `1646740800000`  | currency fees in the last 24h price: currency price in USD |
| `timeStamp`      | `1646740800000`  | price change in the last 24h (percentage)                  |
| `volume`         | `0`              | number of the transactions in the last 24h                 |

### Example

```
 app.post('/currencies/:currencies/prices', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/prices`,
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

{% swagger method="post" path="/{currencies}/volume" baseUrl="https://api.flatqube.io/v1/currencies" summary="DEX currency volume" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "data": "524.759033605461",
    "timestamp": 1647273600000
  },
  {
    "data": "1453.839953245414",
    "timestamp": 1647277200000
  },
  {
    "data": "75.106239452670",
    "timestamp": 1647280800000
  },
  ...
]
```
{% endswagger-response %}
{% endswagger %}

This function gets currency volume data info.

It can be used for graphic representation of trading volume (in USD) that has changed over the required period of time.

### Response fields explanation

| Field name  | Example value    | Comment                                                                                                       |
| ----------- | ---------------- | ------------------------------------------------------------------------------------------------------------- |
| `data`      | `4.471446924792` | trading volume at the given moment inside of the given time span, based on the timeframe (hourly, daily etc.) |
| `timestamp` | `1647259200000`  | date-time of the retrieved trading volume data                                                                |

### Request parameters

_Currencies parameter required - represents address of a specific currency._

_Value used for testing is Dai Stablecoin address: 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9_

_Body required. Data example used for Postman tests:_

| Field name  | Example value                                               | Comment                                                                              |
| ----------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `from`      | `1646741858511` or `March 8, 2022 12:17:38.511 PM GMT time` | Date-time in UNIX format for the start of desired timespan                           |
| `timeframe` | `“H1”, “D1”`                                                | Desired timeframe to retrieve trading volume data, could be set for hours, days, etc |
| `to`        | `1647346658513` or `March 15, 2022 12:17:38.513 PM`         | Date-time in UNIX format for the end of timespan                                     |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### Example

```javascript
app.post('/currencies/:currencies/volume', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/volume`,
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

{% swagger method="post" path="{currencies}/tvl" baseUrl="https://api.flatqube.io/v1/currencies/" summary="Currency tvl data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
 {
    "data": "443050.967523733272",
    "timestamp": 1647302400000
  },
  {
    "data": "443050.967523733272",
    "timestamp": 1647306000000
  },
  {
    "data": "443050.967523733272",
    "timestamp": 1647309600000
  },
  ...
  ]
```
{% endswagger-response %}
{% endswagger %}

This function gets currency volume data info.

It can be used for graphic representation of trading volume (in USD) that has changed over the required period of time.

### Request parameters

_Currencies parameter required - represents address of a specific currency._

_Value used for testing is Dai Stablecoin address: 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9_

_The example data used for Postman tests:_

| Field name | Example value                                               | Comment                                                    |
| ---------- | ----------------------------------------------------------- | ---------------------------------------------------------- |
| `from`     | `1646741858511` or `March 8, 2022 12:17:38.511 PM GMT time` | Date-time in UNIX format for the start of desired timespan |
| `to`       | `1647346658513` or `March 15, 2022 12:17:38.513 PM`         | Date-time in UNIX format for the end of timespan           |

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### Response fields explanation

| Field name  | Example volume        | Comment                                                                                              |
| ----------- | --------------------- | ---------------------------------------------------------------------------------------------------- |
| `data`      | `433345.034717907965` | TVL for the given moment inside of the given time span, based on the timeframe (hourly, daily, etc.) |
| `timestamp` | `1647244800000`       | Date time of the retrieved trading volume data                                                       |

### Example

```javascript
app.post('/currencies/:currencies/tvl', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/tvl`,
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
