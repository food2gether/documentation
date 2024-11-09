# Account Service

## GET `/accounts/`

Returns a list of all accounts.

### Headers
_None_

### Parameters
_None_

### Response
| Status Code | Description                        | Example Response Body                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Account found                      | <pre lang="json">{<br>  "success": true,<br>  "data": \[<br>    {<br>      "id": 1731095302112,<br>      "name": "max_mustermann",<br>      "displayname": "Max Mustermann",<br>      "avatar_url": "https://food2gether.com/api/accounts/1731095302112/avatar",<br>      "contact": \[<br>        {<br>          "displayname": "E-Mail",<br>          "value": "max.mustermann@example.com"<br/>        },<br>        {<br>          "displayname": "Phone",<br>          "value": "+49 1568 483234"<br/>        }<br>      ]<br/>    },<br>    {<br>      "id": 1099871596193,<br>      "name": "phro",<br>      "displayname": "Dr. Philipp Rohde",<br>      "avatar_url": "https://food2gether.com/api/accounts/1099871596193/avatar",<br>      "contact": \[<br>        {<br>          "displayname": "E-Mail",<br>          "value": "rhode@fh-aachen.com"<br/>        },<br>        {<br>          "displayname": "Discord",<br>          "value": "phro#3865"<br/>        }<br>      ]<br/>    }<br>  ]<br/>}</pre> |

### Example Request
```shell
curl --request POST https://food2gether.com/api/accounts \
     --header 'Content-Type: application/json'
```

## GET `/accounts/:id`

Returns the account with the given ID/username.

### Headers
_None_

### Parameters
| Key  | Type           | Required | Description                  |
|------|----------------|----------|------------------------------|
| `id` | `int`/`String` | `true`   | The ID of the account to get |

### Response
| Status Code | Description                        | Example Response Body                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 200         | Account found                      | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731095302112,<br>    "name": "max_mustermann",<br>    "displayname": "Max Mustermann",<br>    "avatar_url": "https://food2gether.com/api/accounts/1731095302112/avatar",<br>    "contact": \[<br>      {<br>        "displayname": "E-Mail",<br>        "value": "max.mustermann@example.com"<br/>      },<br>      {<br>        "displayname": "Phone",<br>        "value": "+49 1568 483234"<br/>      }<br>    ]<br/>  }<br>}</pre> |
| 404         | Login failed (Invalid credentials) | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 404,<br>    "message_key": "account.notfound"<br>  }<br>}</pre>                                                                                                                                                                                                                                                                                                                                                                     |

### Example Request
```shell
curl --request POST https://food2gether.com/api/accounts/1731095302112 \
     --header 'Content-Type: application/json'
```

## PUT `/accounts/`

Creates a new account.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Authorization` | `Basic <email:password \| base64>` |

### Parameters
| Key           | Type                                          | Required | Description                                |
|---------------|-----------------------------------------------|----------|--------------------------------------------|
| `name`        | `String`                                      | `true`   | A unique username                          |
| `displayname` | `String`                                      | `true`   | The display name of the user               |
| `contact`     | `Array<{displayname: String, value: String}>` | `true`   | An array of contact information            |
| `avatar`      | `Base64`                                      | `false`  | Avatar image data as base64-encoded string |

### Response
| Status Code | Description   | Example Response Body                                                                                                                        |
|-------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 201         | Account found | <pre lang="json">{<br>  "success": true,<br>  "data": {<br>    "id": 1731095302112,<br/>  }<br>}</pre>                                       |
| 401         | Unauthorized  | <pre lang="json">{<br>  "success": false,<br>  "error": {<br>    "code": 401,<br>    "message_key": "authorization.failed"<br>  }<br>}</pre> |

### Example Request
```shell
curl --request PUT https://food2gether.com/api/accounts/ \
     --header 'Content-Type: application/json' \
     --header 'Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQK' \
     --data @- << EOF
{
  "name": "max_mustermann",
  "displayname": "Max Mustermann",
  "contact": [
    {
      "displayname": "MS Teams",
      "value": "mamu"
    }
  ],
  "avatar": "data:image/svg+xml;base64,PD94bWwgdmVyc2lv..."
}
EOF
```