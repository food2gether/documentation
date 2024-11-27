# Session Service

## PUT `/api/v1/sessions/`

Creates/Updates a session.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |
| `Content-Type`  | `application/json`                 |

### Parameters
When `id` is omitted, a new session is created. In this case all other arguments are required. When `id` is provided, the session with the given ID is updated.

| Key             | Type   | Required | Description                                    |
|-----------------|--------|----------|------------------------------------------------|
| `id`            | `int`  | `false`  | The ID of the session to update                |
| `restaurant_id` | `int`  | `false`  | The restaurant where the orders will be placed |
| `organizer_id`  | `int`  | `false`  | The responsible person                         |
| `deadline`      | `Date` | `false`  | The deadline for the orders                    |

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
      <td>Bad Request</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 400,
    "message_key": "request.invalid"
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
curl --request PUT https://food2gether.com/api/v1/sessions/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json' \ 
     --data @- << EOF
{
  "restaurant_id": 1,
  "organizer_id": 1,
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
  "data": [
    {
      "restaurant_id": 1,
      "organizer_id": 1,
      "deadline": "2024-11-10T00:25:08.337Z"
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
  "data": {
    "restaurant_id": 1,
    "organizer_id": 1,
    "deadline": "2024-11-10T00:25:08.337Z"
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
  "error": {
    "code": 404,
    "message_key": "session.not_found"
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
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

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
  "data": {
    "restaurant_id": 1,
    "organizer_id": 1,
    "deadline": "2024-11-10T00:25:08.337Z"
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
    <tr>
      <td>404</td>
      <td>Not Found</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 404,
    "message_key": "session.not_found"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl --request DELETE https://food2gether.com/api/v1/sessions/688713425/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```
