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
| Status Code | Description  | Example Response Body                                                                                                                        |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Updated      | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346<br>  }<br>}</pre>                                            |
| 201         | Created      | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731155346<br>  }<br>}</pre>                                            |
| 400         | Bad Request  | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 400,<br>    "message_key": "request.invalid<br>  }<br>}</pre>       |
| 401         | Unauthorized | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre> |

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
| Status Code | Description | Example Response Body                                                                                                                                                                                                     |
|-------------|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Ok          | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br/>    {<br/>      "restaurant_id": 1,<br/>      "organizer_id": 1,<br/>      "deadline": "2024-11-10T00:25:08.337Z",<br/>    },<br/>    ...<br/>  ]<br>}</pre> |

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
| Status Code | Description | Example Response Body                                                                                                                                                             |
|-------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Ok          | <pre lang="json">{<br>  "success": true,<br>  "data": {<br/>    "restaurant_id": 1,<br/>    "organizer_id": 1,<br/>    "deadline": "2024-11-10T00:25:08.337Z",<br/>  }<br>}</pre> |
| 404         | Not Found   | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "session.not_found"<br>  }<br>}</pre>                                         |

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
| Status Code | Description  | Example Response Body                                                                                                                                                             |
|-------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Ok           | <pre lang="json">{<br>  "success": true,<br>  "data": {<br/>    "restaurant_id": 1,<br/>    "organizer_id": 1,<br/>    "deadline": "2024-11-10T00:25:08.337Z",<br/>  }<br>}</pre> |
| 401         | Unauthorized | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre>                                      |
| 404         | Not Found    | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "session.not_found"<br>  }<br>}</pre>                                         |

### Example Request
```shell
curl --request DELETE https://food2gether.com/api/v1/sessions/688713425/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```