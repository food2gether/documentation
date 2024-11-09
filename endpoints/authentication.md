# Authentication Service

Creates a new user account.

## PUT `/authentication/`

### Headers
_None_

### Parameters
| Key        | Type     | Required | Description                                   |
|------------|----------|----------|-----------------------------------------------|
| `email`    | `String` | `true`   | The email of the user to be authenticated.    |
| `password` | `String` | `true`   | The password of the user to be authenticated. |
| `email`    | `String` | `true`   | The email of the user to be authenticated.    |

### Response
| Status Code | Description               | Example Response Body                                                                                                                       |
|-------------|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| 201         | User created successfully | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "token": "&lt;session_token&gt;"<br>  }<br>}</pre>                           |
| 409         | User already exists       | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 409,<br>    "message_key": "registration.failed"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/authentication/ \
     --header 'Content-Type: application/json' \
     --data @- << EOF
{
    "username": "username",
    "password": "password",
    "email": "user@example.com"
}
EOF
```

## POST `/authentication/`

Login with an existing user account.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

### Parameters
_None_

### Response
| Status Code | Description                        | Example Response Body                                                                                                                         |
|-------------|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Login succeeded                    | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "token": "&lt;session_token&gt;"<br>  }<br>}</pre>                             |
| 401         | Login failed (Invalid credentials) | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authentication.failed"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request POST https://food2gether.com/api/authentication/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json'
```

## DELETE `/authentication/`

Logout with an existing user account.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

### Parameters
_None_

### Response
| Status Code | Description             | Example Response Body                                                                                                                         |
|-------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Successfully logged out | <pre lang="json">{<br>  "success": true,<br>  "data": null<br>}</pre>                                                                         |
| 401         | Unauthorized            | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authentication.failed"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request POST https://food2gether.com/api/authentication/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json'
```