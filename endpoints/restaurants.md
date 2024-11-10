# Restaurant Service

## PUT `/api/v1/restaurantes/`

Creates/Updates a restaurant.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |
| `Content-Type`  | `application/json`                 |

### Parameters
When `id` is omitted, a new restaurant is created. In this case all other arguments are required. When `id` is provided, the restaurant with the given ID is updated.

| Key           | Type                                                         | Required | Description                        |
|---------------|--------------------------------------------------------------|----------|------------------------------------|
| `id`          | `int`                                                        | `false`  | The ID of the restaurant to update |
| `displayname` | `String`                                                     | `false`  | The displayname of the restaurant  |
| `address`     | `{street: String, number: int, city: String, postcode: int}` | `false`  | The address of the restaurant      |

### Response
| Status Code | Description       | Example Response Body                                                                                                                            |
|-------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Updated           | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346<br>  }<br>}</pre>                                                |
| 201         | Created           | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346<br>  }<br>}</pre>                                                |
| 400         | Missing arguments | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "request.missingarguments"<br>  }<br>}</pre> |
| 401         | Unauthorized      | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre>     |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/restaurantes/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json' \ 
     --data @- << EOF
{
  "displayname": "Restaurant",
  "address": {
    "street": "Musterstraße", 
    "number": 42, 
    "city": "Musterstadt", 
    "postalcode": 12345
  }
}
EOF
```

## GET `/api/v1/restaurantes/`

Gets all restaurants.

### Headers
_None_

### Parameters
| Key      | Type     | Required | Description                     |
|----------|----------|----------|---------------------------------|
| `search` | `String` | `false`  | Query for searching restaurants |

### Response
| Status Code | Description | Example Response Body                                                                                                                                                                                                                                                                                                        |
|-------------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Found       | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br>    {<br>      "id": 1731155346,<br>      "displayname": "Fat Baby",<br/>      "address": {<br/>        "street": Musterstr.",<br>        "number": 42,<br>        "city": "Aachen",<br>        "postalcode": 52072<br>      },<br/>      ...<br/>  ]<br>}</pre> |

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/restaurantes?search=Fat%20Baby \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```

## GET `/api/v1/restaurantes/:id/`

Gets a specific restaurant.

### Headers
_None_

### Parameters
| Key  | Type  | Required | Description              |
|------|-------|----------|--------------------------|
| `id` | `int` | `true`   | The id of the restaurant |

### Response
| Status Code | Description | Example Response Body                                                                                                                                                                                                                                                              |
|-------------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Found       | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346,<br>    "displayname": "Fat Baby",<br/>    "address": {<br/>      "street": Musterstr.",<br>      "number": 42,<br>      "city": "Aachen",<br>      "postalcode": 52072<br>    }<br>  }<br>}</pre> |
| 404         | Not found   | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "restaurant.notfound"<br>  }<br>}</pre>                                                                                                                                        |

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/restaurantes/1731155346 \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```

## DELETE `/api/v1/restaurantes/:id/`

Deletes a specific restaurant.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

### Parameters
| Key  | Type  | Required | Description              |
|------|-------|----------|--------------------------|
| `id` | `int` | `true`   | The id of the restaurant |

### Response
| Status Code | Description | Example Response Body                                                                                                                       |
|-------------|-------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Ok          | <pre lang="json">{<br>  "success": true,<br>  "data": null<br>}</pre>                                                                       |
| 404         | Not found   | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "restaurant.notfound"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request DELETE https://food2gether.com/api/v1/restaurantes/1731155346 \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```

<!-- Menues -->

## PUT `/api/v1/restaurantes/:id/menu/`

Updates the menu of an existing restaurant.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |
| `Content-Type`  | `application/json`                 |

### Parameters
| Key       | Type                                                                                            | Required | Description                                 |
|-----------|-------------------------------------------------------------------------------------------------|----------|---------------------------------------------|
| `id`      | `int`                                                                                           | `true`   | The ID of the restaurant                    |
| `entries` | `Array<{id: String, name: String, description: String, price: int, allergies: Array<Allergy>}>` | `false`  | The menu entries related to this restaurant |

### Response
| Status Code | Description          | Example Response Body                                                                                                                        |
|-------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Updated              | <pre lang="json">{<br>  "success": true,<br>  "data": null<br>}</pre>                                                                        |
| 401         | Unauthorized         | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre> |
| 404         | Restaurant not found | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "menu.notfound"<br>  }<br>}</pre>        |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/restaurantes/1731155346/menu \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json' \
     --data @- << EOF
{
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

## GET `/api/v1/restaurantes/:id/menu/`

Gets the menu of a specific restaurant.

### Headers
_None_

### Parameters
| Key  | Type  | Required | Description              |
|------|-------|----------|--------------------------|
| `id` | `int` | `true`   | The id of the restaurant |

### Response
| Status Code | Description          | Example Response Body                                                                                                                                                                                                                                                                                                                                          |
|-------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Found                | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br/>    {<br/>      "id": "1",<br/>      "name": "Springrolles",<br/>      "description": "Asian fried vegetable rolls",<br/>      "price": 349,<br/>      "allergies": \[<br/>        "VEGETARIAN",<br/>        "VEGAN",<br/>        "PEANUTS"<br/>      ]<br/>    },<br/>    ...<br/>  ]<br>}</pre> |
| 404         | Restaurant not found | <pre lang="json">{<br/>  "success": false,<br/>  "error": {<br/>    "code": 404,<br/>    "message_key": "restaurant.notfound"<br/>  }<br/>}</pre>                                                                                                                                                                                                              |

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/restaurantes/1731155346/menu \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```