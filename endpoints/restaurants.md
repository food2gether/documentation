# Restaurant Service

## PUT `/api/v1/restaurantes/`

Creates/Updates a restaurant.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Content-Type`  | `application/json`                 |

### Parameters
When `id` is omitted, a new restaurant is created. In this case all other arguments are required. When `id` is provided, the restaurant with the given ID is updated.

| Key           | Type                                                               | Required | Description                        |
|---------------|--------------------------------------------------------------------|----------|------------------------------------|
| `id`          | `int`                                                              | `false`  | The ID of the restaurant to update |
| `displayName` | `String`                                                           | `false`  | The displayname of the restaurant  |
| `address`     | `{street: String, city: String, postalCode: int, country: String}` | `false`  | The address of the restaurant      |

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
  "status": 200,
  "data": {
    "id": 1,
    "displayName": "Habibna",
    "address": {
      "street": "Ahorn Str. 1",
      "city": "Aachen",
      "postalCode": "52072",
      "country": "Germany"
    }
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
  "status": 201,
  "data": {
    "id": 1,
    "displayName": "Mensa Ahorn",
    "address": {
      "street": "Ahorn Str. 1",
      "city": "Aachen",
      "postalCode": "52072",
      "country": "Germany"
    }
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
  "status": 400,
  "message": "Restaurant display name and address must not be null"
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        <pre lang="json">
        </pre>
      </td>
    </tr>
  </tbody>
</table>


### Example Request
```shell
curl -X 'PUT' \
  'http://localhost:8080/api/v1/restaurants' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 9007199254740991,
  "displayName": "string",
  "address": {
    "street": "string",
    "city": "string",
    "postalCode": "string",
    "country": "string"
  }
}'
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
  "status": 200,
  "data": [
    {
      "id": 1,
      "displayName": "Habibna",
      "address": {
        "street": "Ahorn Str. 1",
        "city": "Aachen",
        "postalCode": "52072",
        "country": "Germany"
      }
    }
  ]
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/restaurants' \
  -H 'accept: */*'
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
  "status": 200,
  "data": {
    "id": 1,
    "displayName": "Habibna",
    "address": {
      "street": "Ahorn Str. 1",
      "city": "Aachen",
      "postalCode": "52072",
      "country": "Germany"
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
  "status": 404,
  "message": "Restaurant not found"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/restaurants/2' \
  -H 'accept: */*'
```

## DELETE `/api/v1/restaurantes/:id/`

Deletes a specific restaurant.

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
      <td>Ok</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "status": 200,
  "data": {
    "id": 1,
    "displayName": "Habibna",
    "address": {
      "street": "Ahorn Str. 1",
      "city": "Aachen",
      "postalCode": "52072",
      "country": "Germany"
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
  "status": 404,
  "message": "Restaurant not found"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl -X 'DELETE' \
  'http://localhost:8080/api/v1/restaurants/5' \
  -H 'accept: */*'
```

<!-- Menues -->

## PUT `/api/v1/restaurantes/:id/menu/`

Updates the menu of an existing restaurant.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Content-Type`  | `application/json`                 |

### Parameters
| Key  | Type                                                                 | Required | Description                                 |
|------|----------------------------------------------------------------------|----------|---------------------------------------------|
| `id` | `int`                                                                | `true`   | The ID of the restaurant                    |
| `[]` | `Array<{id: String, name: String, description: String, price: int}>` | `true`   | The menu entries related to this restaurant |

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
  "status": 200,
  "data": [
    {
      "id": 3,
      "restaurantId": 1,
      "name": "Schawama",
      "description": "Is legga",
      "price": 500
    }
  ]
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        <pre lang="json">
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
  "status": 404,
  "message": "Restaurant not found"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl -X 'PUT' \
  'http://localhost:8080/api/v1/restaurants/1/menu' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '[
  {
    "name": "Schawama",
    "description": "Is legga",
    "price": 500
  }
]'
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
  "status": 200,
  "data": [
    {
      "id": 3,
      "restaurantId": 1,
      "name": "Schawama",
      "description": "Is legga",
      "price": 500
    }
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
  "status": 404,
  "message": "Restaurant not found"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>
                                                                                           |

### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/restaurants/1/menu' \
  -H 'accept: */*'
```
