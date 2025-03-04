# Session Service

## PUT `/api/v1/sessions/`

Creates/Updates a session.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Content-Type`  | `application/json`                 |

### Parameters
When `id` is omitted, a new session is created. In this case all other arguments are required. When `id` is provided, the session with the given ID is updated.

| Key             | Type       | Required | Description                                    |
|-----------------|------------|----------|------------------------------------------------|
| `id`            | `int`      | `false`  | The ID of the session to update                |
| `restaurantId`  | `int`      | `false`  | The restaurant where the orders will be placed |
| `organizerId`   | `int`      | `false`  | The responsible person                         |
| `deadline`      | `DateTime` | `false`  | The deadline for the orders                    |

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
    "id": 6,
    "restaurantId": 1,
    "organizerId": 1,
    "deadline": "2025-03-10T12:15:50"
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
    "id": 6,
    "restaurantId": 1,
    "organizerId": 1,
    "deadline": "2025-03-10T12:15:50"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 404,
  "message": "Session with id 999 does not exist"
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl -X 'PUT' \
  'http://localhost:8080/api/v1/sessions' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
"id": 999,
  "restaurantId": 1,
  "organizerId": 1,
  "deadline": "2025-03-10T12:15:50"
}'
```

## GET `/api/v1/sessions/`

Gets all sessions with optional filters.

### Headers
_None_

### Parameters
| Key             | Type      | Required | Description                                           |
|-----------------|-----------|----------|-------------------------------------------------------|
| `restaurant_id` | `int`     | `false`  | Filter for a specific restaurant                      |
| `orderable`     | `boolean` | `false`  | Filter for sessions with their deadline in the future |

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
  "data": [
    {
      "id": 5,
      "restaurantId": 1,
      "organizerId": 1,
      "deadline": "2025-03-10T12:15:50"
    },
    {
      "id": 6,
      "restaurantId": 1,
      "organizerId": 1,
      "deadline": "2025-03-10T12:15:50"
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
  'http://localhost:8080/api/v1/sessions?orderable=true&restaurant_id=1' \
  -H 'accept: */*'
```

## GET `/api/v1/sessions/:id/`

Gets a session by its ID.

### Headers
_None_

### Parameters
| Key  | Type  | Required | Description    |
|------|-------|----------|----------------|
| `id` | `int` | `true`   | The session id |

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
    "id": 4,
    "restaurantId": 1,
    "organizerId": 1,
    "deadline": "2025-03-10T12:15:50"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Not Found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 404,
  "message": "Session with id 4 does not exist"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/sessions/4' \
  -H 'accept: */*'
```

## DELETE `/api/v1/sessions/:id/`

Removes a session by its ID.

### Headers
_None_

### Parameters
| Key  | Type  | Required | Description    |
|------|-------|----------|----------------|
| `id` | `int` | `true`   | The session id |

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
    "id": 4,
    "restaurantId": 1,
    "organizerId": 1,
    "deadline": "2025-03-10T12:15:50"
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
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Not Found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 404,
  "message": "Session with id 4 does not exist"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl --request DELETE https://food2gether.com/api/v1/sessions/688713425/
```

## PUT `/api/v1/sessions/:id/orders/`

Creates/Updates an order.

### Headers

| Key             | Description                        |
|-----------------|------------------------------------|
| `Content-Type`  | `application/json`                 |

### Parameters

When `id` is omitted, a new order is created. In this case all other arguments are required. When `id` is provided, the
order with the given ID is updated.

| Key          | Type                                                                                            | Required | Description                            |
|--------------|-------------------------------------------------------------------------------------------------|----------|----------------------------------------|
| `id`         | `int`                                                                                           | `false`  | The ID of the order                    |
| `profile_id` | `int`                                                                                           | `false`  | The Person behind the order            |
| `entries`    | `Array<{id: String, name: String, description: String, price: int, allergies: Array<Allergy>}>` | `false`  | The menu entries related to this order |

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
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 10
      }
    ],
    "profileId": 1,
    "state": "OPEN"
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
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 10
      }
    ],
    "profileId": 1,
    "state": "OPEN"
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
  "message": "Order with id 123 does not exist"
}
</pre>
      </td>
    </tr>
    <tr>
      <td>400</td>
      <td>Bad request</td>
      <td>
        <pre lang="json">
{
  "objectName": "DTO",
  "attributeName": "state",
  "line": 9,
  "column": 12,
  "value": "NONE"
}
</pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        <pre lang="json"></pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request

```shell
curl -X 'PUT' \
  'http://localhost:8080/api/v1/sessions/5/orders' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "items": [
    {
      "menuItemId": 1,
      "quantity": 10
    }
  ],
  "profileId": 1,
  "state": "OPEN"
}'
```

## GET `/api/v1/sessions/:id/orders/`

Gets all orders with optional filters.

### Headers

_None_

### Parameters

| Key          | Type      | Required | Description                   |
|--------------|-----------|----------|-------------------------------|
| `id`         | `int`     | `true`   | The session id                |
| `profile_id` | `boolean` | `false`  | Filter for a specific profile |

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
  "data": [
    {
      "id": 1,
      "items": [
        {
          "id": 1,
          "menuItemId": 1,
          "quantity": 10
        }
      ],
      "profileId": 1,
      "state": "OPEN"
    }
  ]
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Not Found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 404,
  "message": "Session with id 21 not found"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request

```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/sessions/21/orders' \
  -H 'accept: */*'
```

## GET `/api/v1/sessions/:sessionId/orders/:id/`

Gets an order by its ID.

### Headers

_None_

### Parameters

| Key         | Type  | Required | Description    |
|-------------|-------|----------|----------------|
| `sessionId` | `int` | `true`   | The session id |
| `id`        | `int` | `true`   | The order id   |

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
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 10
      }
    ],
    "profileId": 1,
    "state": "OPEN"
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
  "message": "Order with id 12 does not exist"
}
</pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request

```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/sessions/1/orders/12' \
  -H 'accept: */*'
```

## DELETE `/api/v1/sessions/:sessionId/orders/:id/`

Removes an order by its ID.

### Headers
_None_

### Parameters

| Key         | Type  | Required | Description    |
|-------------|-------|----------|----------------|
| `sessionId` | `int` | `true`   | The session id |
| `id`        | `int` | `true`   | The order id   |

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
    "id": 3,
    "items": [
      {
        "id": 3,
        "menuItemId": 1,
        "quantity": 10
      }
    ],
    "profileId": 1,
    "state": "OPEN"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>403</td>
      <td>Forbidden</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 403,
  "message": "Only the user who owns the order can delete it"
}
</pre>
      </td>
    </tr>
    <tr>
      <td>404</td>
      <td>Not Found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 404,
  "message": "Order with id 2 does not exist"
}
</pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request

```shell
curl -X 'DELETE' \
  'http://localhost:8080/api/v1/sessions/2/orders/3' \
  -H 'accept: */*'
```
