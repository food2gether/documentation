# Authentication Service

Creates a new user account.

## PUT `/api/v1/authentication/`

### Headers
_None_

### Parameters
| Key        | Type     | Required | Description                                   |
|------------|----------|----------|-----------------------------------------------|
| `email`    | `String` | `true`   | The email of the user to be authenticated.    |
| `password` | `String` | `true`   | The password of the user to be authenticated. |

### Response
| Status Code | Description               | Example Response Body                                                                                                                       |
|-------------|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| 201         | User created successfully | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "token": "&lt;session_token&gt;"<br>  }<br>}</pre>                           |
| 409         | User already exists       | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 409,<br>    "message_key": "registration.failed"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/authentication/ \
     --header 'Content-Type: application/json' \
     --data @- << EOF
{
    "password": "password",
    "email": "user@example.com"
}
EOF
```

## POST `/api/v1/authentication/`

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
curl --request POST https://food2gether.com/api/v1/authentication/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```

## DELETE `/api/v1/authentication/`

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
curl --request DELETE https://food2gether.com/api/v1/authentication/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK'
```

## PUT `/api/v1/authentication/reset/`

Requests a password reset for an existing user account.

### Headers
_None_

### Parameters
| Key     | Type     | Required | Description                                      |
|---------|----------|----------|--------------------------------------------------|
| `email` | `String` | `true`   | The email of the user to reset the password for. |

### Response
| Status Code | Description      | Example Response Body                                                                                                                    |
|-------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Request received | <pre lang="json">{<br>  "success": true,<br>  "data": null<br>}</pre>                                                                    |
| 404         | Not found        | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "account.notfound"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/authentication/reset \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --form 'email=max.mustermann@gmail.com'
```

## POST `/api/v1/authentication/reset/`

Resets a password for an existing user account.

### Headers
| Key             | Description                      |
|-----------------|----------------------------------|
| `Authorization` | `Bearer <reset_token>`           |

### Parameters
| Key        | Type     | Required | Description      |
|------------|----------|----------|------------------|
| `password` | `String` | `true`   | The new password |

### Response
| Status Code | Description   | Example Response Body                                                                                                                 |
|-------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Successful    | <pre lang="json">{<br>  "success": true,<br>  "data": null<br>}</pre>                                                                 |
| 400         | Invalid token | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 400,<br>    "message_key": "token.invalid"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/authentication/ \
     --header 'Authorization: Bearer dXNlcm5hbWU6cGFzc3456ujhgfd3545dvcmQK'
     --form 'password=newpassword'
```