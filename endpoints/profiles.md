# Profiles Service

## GET `/api/v1/profiles/`

Returns a list of all profiles.

### Headers
_None_

### Parameters
| Key    | Type     | Required | Description             |
|--------|----------|----------|-------------------------|
| search | `String` | `false`  | The search query string |

### Response
| Status Code | Description   | Example Response Body                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Profile found | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br>    {<br>      "id": 1731095302112,<br>      "name": "max_mustermann",<br>      "displayname": "Max Mustermann",<br>      "contact": \[<br>        {<br>          "displayname": "E-Mail",<br>          "value": "max.mustermann@example.com"<br/>        },<br>        {<br>          "displayname": "Phone",<br>          "value": "+49 1568 483234"<br/>        }<br>      ]<br/>    },<br>    {<br>      "id": 1099871596193,<br>      "name": "phro",<br>      "displayname": "Dr. Philipp Rohde",<br>      "contact": \[<br>        {<br>          "displayname": "E-Mail",<br>          "value": "rhode@fh-aachen.com"<br/>        },<br>        {<br>          "displayname": "Discord",<br>          "value": "phro#3865"<br/>        }<br>      ]<br/>    }<br>  ]<br/>}</pre> |

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/profiles/
```

## GET `/api/v1/profiles/:id`

Returns the profile with the given ID/username.

### Headers
_None_

### Parameters
| Key  | Type           | Required | Description                  |
|------|----------------|----------|------------------------------|
| `id` | `int`/`String` | `true`   | The ID of the profile to get |

### Response
| Status Code | Description   | Example Response Body                                                                                                                                                                                                                                                                                                                                                                                                      |
|-------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Account found | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731095302112,<br>    "name": "max_mustermann",<br>    "displayname": "Max Mustermann",<br>    "contact": \[<br>      {<br>        "displayname": "E-Mail",<br>        "value": "max.mustermann@example.com"<br/>      },<br>      {<br>        "displayname": "Phone",<br>        "value": "+49 1568 483234"<br/>      }<br>    ]<br/>  }<br>}</pre> |
| 404         | Not found     | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "account.notfound"<br>  }<br>}</pre>                                                                                                                                                                                                                                                                                   |

### Example Request
```shell
curl --request GET https://food2gether.com/api/v1/accounts/1731095302112
```

## PUT `/api/v1/accounts/`

Creates/Updates a profile.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |
| `Content-Type`  | `application/json`                 |

### Parameters
When `id` is omitted, a new profile is created. In this case all other arguments are required. When `id` is provided, the profile with the given ID is updated. \
The `name` field is ignored when updating a profile.

| Key           | Type                                          | Required | Description                                |
|---------------|-----------------------------------------------|----------|--------------------------------------------|
| `id`          | `int`/`String`                                | `false`  | The ID/username of the profile to update   |
| `name`        | `String`                                      | `false`  | A unique username                          |
| `displayname` | `String`                                      | `false`  | The display name of the user               |
| `contact`     | `Array<{displayname: String, value: String}>` | `false`  | An array of contact information            |

### Response
| Status Code | Description                             | Example Response Body                                                                                                                            |
|-------------|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Updated                                 | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731095302112,<br/>  }<br>}</pre>                                           |
| 201         | Created                                 | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731095302112,<br/>  }<br>}</pre>                                           |
| 400         | Missing arguments                       | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 400,<br>    "message_key": "request.missingarguments"<br>  }<br>}</pre> |
| 401         | Unauthorized                            | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre>     |
| 403         | Username already exists                 | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 403,<br>    "message_key": "user.exists"<br>  }<br>}</pre>              |
| 409         | Profile already associated with account | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 409,<br>    "message_key": "account.exists"<br>  }<br>}</pre>           |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/accounts/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --header 'Content-Type: application/json' \
     --data @- << EOF
{
  "name": "max_mustermann",
  "displayname": "Max Mustermann",
  "contact": [
    {
      "displayname": "MS Teams",
      "value": "mamu"
    }
  ]
}
EOF
```

## DELETE `/api/v1/accounts/:id/`

Deletes a profile.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

### Parameters
| Key           | Type                                          | Required | Description                              |
|---------------|-----------------------------------------------|----------|------------------------------------------|
| `id`          | `int`/`String`                                | `true`   | The ID/username of the profile to update |

### Response
| Status Code | Description  | Example Response Body                                                                                                                        |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Deleted      | <pre lang="json">{<br>  "success": true,<br>  "data": null<br>}</pre>                                                                        |
| 401         | Unauthorized | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/v1/accounts/ \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
```