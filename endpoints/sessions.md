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
  "status": 200,
  "data": {
    "id": 73683,
    "restaurantId": 123,
    "organizerId": 123,
    "deadline": "2024-10-01T10:00:00"
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
  "status": 201,
  "data": {
    "id": 73683,
    "restaurantId": 123,
    "organizerId": 123,
    "deadline": "2024-10-01T10:00:00"
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
  "status": 400,
  "error": {
    "message": "request.invalid"
  }
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
curl --request PUT https://food2gether.com/api/v1/sessions/ \
     --header 'Content-Type: application/json' \ 
     --data @- << EOF
{
  "restaurantId": 1,
  "organizerId": 1,
  "deadline": "2024-11-10T00:25:08.337Z"
}
EOF
```

## GET `/api/v1/sessions/`

Gets all sessions with optional filters.

### Headers
_None_

### Parameters
| Key             | Type      | Required | Description                      |
|-----------------|-----------|----------|----------------------------------|
| `restaurant_id` | `int`     | `false`  | Filter for a specific restaurant |
| `orderable`     | `boolean` | `false`  | Filter for running sessions      |

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
      "restaurantId": 1,
      "organizerId": 1,
      "deadline": "2025-02-27T10:38:16.14005047"
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
curl --request GET https://food2gether.com/api/v1/sessions/
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
    "id": 123,
    "restaurantId": 1,
    "organizerId": 1,
    "deadline": "2025-02-27T10:38:43.347245067"
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
  "error": {
    "message": "session.not_found"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/sessions/688713425/
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
    "id": 123,
    "restaurantId": 1,
    "organizerId": 1,
    "deadline": "2025-02-27T10:41:28.979825433"
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
  "code": 404,
  "error": {
    "message": "session.not_found"
  }
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
    "id": 123,
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 10
      }
    ],
    "profileId": 123,
    "state": "REJECTED"
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
    "id": 123,
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 10
      }
    ],
    "profileId": 123,
    "state": "REJECTED"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        <pre lang="json">{
  "success": false,
  "error": {
    "code": 400,
    "detail": "request.invalid"
  }
}</pre>
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
curl --request PUT https://food2gether.com/api/v1/sessions/123/orders \
     --header 'Content-Type: application/json' \
     --data @- << EOF
{
  "id": 1731095302112,
  "profileId": 123,
  "state": "REJECTED",
  "items": [
    {
      "id": 1,
      "menuItemId": 1,
      "quantity": 10
    }
  ]
}
EOF
```

## GET `/api/v1/sessions/:id/orders/`

Gets all orders with optional filters.

### Headers

_None_

### Parameters

| Key          | Type      | Required | Description                   |
|--------------|-----------|----------|-------------------------------|
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
      <td>Found</td>
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
          "quantity": 1
        }
      ],
      "profileId": 1,
      "state": "SUBMITTED"
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
curl --request GET https://food2gether.com/api/v1/sessions/123/orders/
```

## GET `/api/v1/sessions/:id/orders/:id/`

Gets an order by its ID.

### Headers

_None_

### Parameters

| Key  | Type  | Required | Description  |
|------|-------|----------|--------------|
| `id` | `int` | `true`   | The order id |

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
    "id": 123,
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 1
      }
    ],
    "profileId": 1,
    "state": "SUBMITTED"
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
  "error": {
    "message": "order.not_found"
  }
}
</pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request

```shell
curl --request GET https://food2gether.com/api/v1/sessions/123/orders/2345345341/
```

## DELETE `/api/v1/sessions/:id/orders/:id/`

Removes an order by its ID.

### Headers
_None_

### Parameters

| Key  | Type  | Required | Description  |
|------|-------|----------|--------------|
| `id` | `int` | `true`   | The order id |

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
    "id": 123,
    "items": [
      {
        "id": 1,
        "menuItemId": 1,
        "quantity": 1
      }
    ],
    "profileId": 1,
    "state": "REJECTED"
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
  "status": 401,
  "error": {
    "detail": "authorization.failed"
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
  "error": {
    "detail": "order.not_found"
  }
}
</pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request

```shell
curl --request DELETE https://food2gether.com/api/v1/sessions/1223/orders/2345345341/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```
