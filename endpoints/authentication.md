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
      <td>201</td>
      <td>User created successfully</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": {
    "token": "&lt;session_token&gt;"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>409</td>
      <td>User already exists</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 409,
    "message_key": "registration.failed"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>


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
      <td>Login succeeded</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "data": {
    "token": "&lt;session_token&gt;"
  }
}
        </pre>
      </td>
    </tr>
    <tr>
      <td>401</td>
      <td>Login failed (Invalid credentials)</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "error": {
    "code": 401,
    "message_key": "authentication.failed"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>


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
      <td>Successfully logged out</td>
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
    "message_key": "authentication.failed"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

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
      <td>Request received</td>
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
    "message_key": "account.notfound"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>


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
      <td>Successful</td>
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
    "code": 400,
    "message_key": "token.invalid"
  }
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>

### Example Request
```shell
curl --request POST https://food2gether.com/api/v1/authentication/ \
     --header 'Authorization: Bearer dXNlcm5hbWU6cGFzc3456ujhgfd3545dvcmQK' \
     --form 'password=newpassword'
```
