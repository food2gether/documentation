# Order Service

## PUT `/api/v1/orders/`

Creates/Updates an order.

### Headers

| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |
| `Content-Type`  | `application/json`                 |

### Parameters

When `id` is omitted, a new order is created. In this case all other arguments are required. When `id` is provided, the
order with the given ID is updated.

| Key          | Type                                                                                            | Required | Description                            |
|--------------|-------------------------------------------------------------------------------------------------|----------|----------------------------------------|
| `id`         | `int`                                                                                           | `false`  | The ID of the order                    |
| `session_id` | `int`                                                                                           | `false`  | The Session of the order               |
| `profile_id` | `int`                                                                                           | `false`  | The Person behind the order            |
| `entries`    | `Array<{id: String, name: String, description: String, price: int, allergies: Array<Allergy>}>` | `false`  | The menu entries related to this order |

### Response

| Status Code | Description  | Example Response Body                                                                                                                        |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Updated      | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346<br>  }<br>}</pre>                                            |
| 201         | Created      | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346<br>  }<br>}</pre>                                            |
| 400         | Bad Request  | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 400,<br>    "message_key": "request.invalid<br>  }<br>}</pre>       |
| 401         | Unauthorized | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre> |

### Example Request

```shell
curl --request PUT https://food2gether.com/api/v1/orders/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json' \
     --data @- << EOF
{
  "session_id": 688713425,
  "profile_id": 1731095302112,
  "entries": [
    {
      "id": "1",
      "name": "Springrolles",
      "description": "Asian fried vegetable rolls",
      "price": 349,
      "allergies": [
        "VEGETARIAN",
        "VEGAN",
        "PEANUTS"
      ]
    }
  ]
}
EOF
```

## GET `/api/v1/orders/`

Gets all orders with optional filters.

### Headers

_None_

### Parameters

| Key          | Type      | Required | Description                   |
|--------------|-----------|----------|-------------------------------|
| `session_id` | `int`     | `false`  | Filter for a specific session |
| `profile_id` | `boolean` | `false`  | Filter for a specific profile |

### Response

| Status Code | Description | Example Response Body                                                                                                                                                          |
|-------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Found       | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br/>    {<br/>      "session_id": 1,<br/>      "profile_id": 1,<br/>      ,<br/>    },<br/>    ...<br/>  ]<br>}</pre> |

### Example Request

```shell
curl --request GET https://food2gether.com/api/v1/orders/
```

## GET `/api/v1/orders/:id/`

Gets an order by its ID.

### Headers

_None_

### Parameters

| Key  | Type  | Required | Description  |
|------|-------|----------|--------------|
| `id` | `int` | `true`   | The order id |

### Response

| Status Code | Description | Example Response Body                                                                                                                                                          |
|-------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Found       | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br/>    {<br/>      "session_id": 1,<br/>      "profile_id": 1,<br/>      ,<br/>    },<br/>    ...<br/>  ]<br>}</pre> |
| 404         | Not found   | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "order.not_found"<br>  }<br>}</pre>                                        |

### Example Request

```shell
curl --request GET https://food2gether.com/api/v1/orders/2345345341/
```

## DELETE `/api/v1/orders/:id/`

Removes an order by its ID.

### Headers

| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

### Parameters

| Key  | Type  | Required | Description  |
|------|-------|----------|--------------|
| `id` | `int` | `true`   | The order id |

### Response

| Status Code | Description  | Example Response Body                                                                                                                        |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Ok           | <pre lang="json">{<br>  "success": true,<br>  "data": {<br/>    "session_id": 1,<br/>    "profile_id": 1,<br/>    ,<br/>  }<br>}</pre>       |
| 401         | Unauthorized | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre> |
| 404         | Not Found    | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "order.not_found"<br>  }<br>}</pre>      |

### Example Request

```shell
curl --request DELETE https://food2gether.com/api/v1/order/2345345341/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```