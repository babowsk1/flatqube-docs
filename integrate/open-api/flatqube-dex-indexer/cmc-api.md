# CMC API

{% swagger method="get" path="" baseUrl="https://api.flatqube.io/v1/cmc/dex" summary="CMC DEX pools info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2_0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6": {
            "base_id": "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2",
            "base_name": "Tether",
            "base_symbol": "USDT",
            "quote_id": "0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6",
            "quote_name": "USD Coin",
            "quote_symbol": "USDC",
            "last_price": "1.001259244956",
            "base_volume": "2210.44204800",
            "quote_volume": "2213.22553600"
    },
    "0:0cfa60f9454b1b619938c4da6a138b1cc62da937b3f6c0506405daf2a88e0115_0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d": {
            "base_id": "0:0cfa60f9454b1b619938c4da6a138b1cc62da937b3f6c0506405daf2a88e0115",
            "base_name": "EUR-Fiat-Based",
            "base_symbol": "EUPI",
            "quote_id": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
            "quote_name": "Wrapped EVER",
            "quote_symbol": "WEVER",
            "last_price": "5.547157916853",
            "base_volume": "359.90566477",
            "quote_volume": "1996.453557649000"
    },
    ...
}
```
{% endswagger-response %}
{% endswagger %}

The function is used to get all information about DEX pools.

It can be used to tabulate all dex pools with their pairs and desired information about them.

### Request parameters

_No parameters are required._

### Response fields explanation

| Field name     | Example value                                                        | Comment                                                         |
| -------------- | -------------------------------------------------------------------- | --------------------------------------------------------------- |
| `base_id`      | `0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2` | Root address of the base token in the certain dex pool          |
| `base_name`    | `Tether`                                                             | Full name of the base token                                     |
| `base_symbol`  | `USDT`                                                               | Full name of the base token                                     |
| `quote_id`     | 0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6   | Root address of the quote token in the pool                     |
| `quote_name`   | `USD Coin`                                                           | Full name of the quote token                                    |
| `quote_symbol` | `USDC`                                                               | Symbol of the quote token                                       |
| `last_price`   | `1.001259244956`                                                     | Price of 1 base token in quote tokens (ie. 1 USDT = 1.001 USDC) |
| `base_volume`  | `2210.44204800`                                                      | Trading volume (in USD) of base token                           |
| `quote_volume` | `2213.22553600`                                                      | Trading volume (in USD) of quote token                          |

### Example

```javascript
  app.get('/cmc/dex', (req, res) => {
        axios({
            method: 'get',
            url: liveApiUrl + '/cmc/dex'
          })
        .then(function (response) {
            res.send(response.data)
        })
        .catch(function(error){
            console.error(error)
            res.send('Error')
        })
  })
```

{% swagger method="get" path="/cmc/farming" baseUrl="https://api.flatqube.io/v1" summary="CMC DEX farming pools info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "provider": "FlatQube",
    "provider_logo": "https://flatqube.io/favicon.svg",
    "provider_URL": "https://flatqube.io",
    "links": [],
    "pools": [{
                "name": "SOON/WEVER",
                "pair": "SOON/WEVER",
                "pairLink": "https://flatqube.io/farming/0:5b297ebf0d4baa84e5e5f2cff61f3563fa94e62e8c93d5a2fd19145d72007bf3",
                "logo": "https://flatqube.io/favicon.svg",
                "poolRewards": ["SOON", "COLA", "BAPBAPA", "GRE"],
                "apr": "3.0815",
                "totalStake": "114846.005396701372"
            }, {
                "name": "USDT/DUSA",
                "pair": "USDT/DUSA",
                "pairLink": "https://flatqube.io/farming/0:2ff5db6e886e337c921154f3de9b77cfcadd1940c84b4f3b97c312c069cd7ea0",
                "logo": "https://flatqube.io/favicon.svg",
                "poolRewards": ["DUSA"],
                "apr": "97.9022",
                "totalStake": "53838.449198250683"
            }, {
                "name": "WEVER/BRIDGE",
                "pair": "WEVER/BRIDGE",
                "pairLink": "https://flatqube.io/farming/0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0",
                "logo": "https://flatqube.io/favicon.svg",
                "poolRewards": ["BRIDGE", "QUBE"],
                "apr": "0.5353",
                "totalStake": "11763741.699148025624"
            },
            ...
    }
```
{% endswagger-response %}
{% endswagger %}

This function helps you get farming pools information:

### **Request parameters**

_No parameters required_

### Response fields explanation

| Field name      | Example value                                                                                                                                                                                      | Comment                                                                                           |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `provider`      | `FlatQube`                                                                                                                                                                                         | Represents provider of the farming pool                                                           |
| `provider_logo` | [`https://flatqube.io/favicon.svg`](https://flatqube.io/favicon.svg)\`\`                                                                                                                           | Path to the provider logo provider                                                                |
| `url`           | https://flatqube.io                                                                                                                                                                                | Url to the provider                                                                               |
| `links`         |                                                                                                                                                                                                    |                                                                                                   |
| `pools`         |                                                                                                                                                                                                    | List of all the pools available on the provider, contains following information about each pool   |
| `name`          | `WEVER/BRIDGE`                                                                                                                                                                                     | Name of the pool in format left pair/right pair                                                   |
| `pair`          | `WEVER/BRIDGE`                                                                                                                                                                                     | Info about which two tokens are in pair for the given pool                                        |
| `pairLink`      | [`https://flatqube.io/farming/0:5b297ebf0d4baa84e5e5f2cff61f3563fa94e62e8c93d5a2fd19145d72007bf3`](https://flatqube.io/farming/0:5b297ebf0d4baa84e5e5f2cff61f3563fa94e62e8c93d5a2fd19145d72007bf3) | URL to the farming pool where you can see all the details about that pool and start farming in it |
| `logo`          | [`https://flatqube.io/favicon.svg`](https://flatqube.io/favicon.svg)\`\`                                                                                                                           |                                                                                                   |
| `poolRewards`   | `BRIDGE, QUBE`                                                                                                                                                                                     | Tokens that are given as a reward for farming in that pool (ie. BRIDGE, QUBE)                     |
| `apr`           | `97.9022`                                                                                                                                                                                          | Apr (Annual Percentage Rate) for farming in that pool                                             |
| `totalStake`    | `53838.449198250683`                                                                                                                                                                               | TVL (Total Value Locked) in USD for the current pool                                              |

### Example

```
app.get('/cmc/farming', (req, res) => {
    axios({
        method: 'get',
        url: liveApiUrl + '/cmc/farming'
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```
