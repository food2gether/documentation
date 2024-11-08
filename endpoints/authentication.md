# Authentication Service

## POST `/`

### Headers
| Key             | Description                           |
|-----------------|---------------------------------------|
| `Authorization` | `Basic <username:password \| base64>` |

### Parameters
_None_

### Cookies
_None_

### Response
| Status Code | Example Response Body                                                                                                                         |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | <pre lang="json">{<br>  "token": "&lt;session_token&gt;",<br>  "success": true<br>}</pre>                                                     |
| 401         | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authentication.failed"<br>  }<br>}</pre> |

## PUT `/`

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <base64 username:password>` |

### Parameters
| Key | Type | Required

### Cookies

### Response