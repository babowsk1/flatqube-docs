# Graphics API

{% swagger method="post" path="/graphic/tvl" baseUrl="http://farming.flatqube.io/v1" summary="Farming pool TVL graphic data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
[
    {
        "data": "19315318.324282999059",
        "timestamp": 1652853600000
    },
...
]
```
{% endswagger-response %}
{% endswagger %}

This method gets farming pool TVL graphic data.

It can be used for graphic representation of total value locked - TVL (in USD) change for the desired period of time. Data required for the request is the farming pool address and the timespan for following the change of total value locked, which is set through the body of the request.

### Request parameters

Body required. Data used for postman tests:

| Filen name         | Example value                                                      | Comment                                                            |
| ------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| farmingPoolAddress | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0 | address of the desired farming pool                                |
| from               | 1646741858511                                                      | date time in UNIX format that represents start of desired timespan |
| timeframe          | H1                                                                 | step of the desired timespan, can be set as hours, days            |
| to                 | 1647346658513                                                      | date time in UNIX format representing the end of desired timespamp |

### Response field explanation

| Field name | Example value         | Comment                                                                      |
| ---------- | --------------------- | ---------------------------------------------------------------------------- |
| data       | 19315318.324282999059 | total balance (in USD) in one farming pool in a concrete moment              |
| timestamp  | 1652853600000         | date time in UNIX format of a concrete moment in which the data is retrieved |

### Example

```
 app.post('/graphic/tvl', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/graphic/tvl`,
        data: {
            farmingPoolAddress: req.body.farmingPoolAddress,
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

{% swagger method="post" path="/graphic/apr" baseUrl="http://farming.flatqube.io/v1" summary="Farming pool APR graphic data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful response " %}
```
[
    {
        "data": "74.5300",
        "timestamp": 1652878800000
    },
    ...
]
```
{% endswagger-response %}
{% endswagger %}

This method gets a farming pool APR graphic data.

It can be used for graphic representation of Annual Percentage Rate - APR (percentage) change for the desired period of time. Data required for the request is the farming pool address and the timespan for following the annual percentage rate change, which is set through the body of the request.

### Request parameters

Body required. Data used for postman tests:

| Field name         | Example value                                                     | Comment                                                            |
| ------------------ | ----------------------------------------------------------------- | ------------------------------------------------------------------ |
| farmingPoolAddress | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff | address of the desired farming pool                                |
| from               | 1646741858511                                                     | date time in UNIX format that represents start of desired timespan |
| timeframe          | H1                                                                | step of the desired timespan, can be set as hours, days            |
| to                 | 1647346658513                                                     | date time in UNIX format representing the end of desired timespan  |

### Response field explanation

| Field name | Example value | Comment                                                                      |
| ---------- | ------------- | ---------------------------------------------------------------------------- |
| data       | 74.5300       | APR (percentage) in one farming pool in a concrete moment                    |
| timestamp  | 1652878800000 | date time in UNIX format of a concrete moment in which the data is retrieved |

### Example

```
 app.post('/graphic/apr', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/graphic/apr`,
        data: {
            farmingPoolAddress: req.body.farmingPoolAddress,
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
