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
<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
      <th>Example Response Body</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>Updated</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": {
    "id": 1731155346
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>201</td>
      <td>Created</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": {
    "id": 1731155346
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>400</td>
      <td>Missing arguments</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 404,
    "message_key": "request.missingarguments"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 401,
    "message_key": "authorization.failed"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>


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
<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
      <th>Example Response Body</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>Found</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": [
    {
      "id": 1731155346,
      "displayname": "Fat Baby",
      "address": {
        "street": "Musterstr.",
        "number": 42,
        "city": "Aachen",
        "postalcode": 52072
      }
    },
    ...
  ]
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

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
<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
      <th>Example Response Body</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>Found</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": {
    "id": 1731155346,
    "displayname": "Fat Baby",
    "address": {
      "street": "Musterstr.",
      "number": 42,
      "city": "Aachen",
      "postalcode": 52072
    }
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Not found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 404,
    "message_key": "restaurant.notfound"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

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
<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
      <th>Example Response Body</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>Ok</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": null
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Not found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 404,
    "message_key": "restaurant.notfound"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

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
<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
      <th>Example Response Body</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>Updated</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": null
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 401,
    "message_key": "authorization.failed"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Restaurant not found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 404,
    "message_key": "menu.notfound"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

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
<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
      <th>Example Response Body</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>Found</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": [
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
    },
    ...
  ]
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Restaurant not found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 404,
    "message_key": "restaurant.notfound"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>
                                                                                           |

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/restaurantes/1731155346/menu \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```
