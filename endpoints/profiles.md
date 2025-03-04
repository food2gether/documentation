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
      <td>Profile found</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "status": 200,
  "data": [
    {
      "id": 1,
      "name": "marvin",
      "displayName": "MarfienGamerXX",
      "profilePictureUrl": "https://fuck-u.com",
      "primaryEmail": "mail@123.xom"
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
  'http://localhost:8080/api/v1/profiles' \
  -H 'accept: */*'
```

## GET `/api/v1/profiles/:id`

Returns the profile with the given ID.

### Headers
_None_

### Parameters
| Key  | Type   | Required | Description                  |
|------|--------|----------|------------------------------|
| `id` | `int`  | `true`   | The ID of the profile to get |

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
      <td>Account found</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "status": 200,
  "data": {
    "id": 1,
    "name": "marvin",
    "displayName": "MarfienGamerXX",
    "profilePictureUrl": "https://fuck-u.com",
    "primaryEmail": "mail@123.xom"
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
  "message": "Profile not found"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>


### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/profiles/2' \
  -H 'accept: */*'
```

## GET `/api/v1/profiles/me`

Returns the own profile with by the `X-User-Email` header. \
The header will be injected by the oauth2 proxy.

### Headers
_None_

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
      <td>Account found</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "status": 200,
  "data": {
    "id": 1,
    "name": "marvin",
    "displayName": "MarfienGamerXX",
    "profilePictureUrl": "https://fuck-u.com",
    "primaryEmail": "mail@123.xom"
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
  "message": "Required Header is missing: X-User-Email"
}
        </pre>
      </td>
    </tr>
  </tbody>
</table>


### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/profiles/me' \
  -H 'accept: */*'
```

## PUT `/api/v1/profiles/`

Creates/Updates a profile.

### Headers
| Key             | Description                        |
|-----------------|------------------------------------|
| `Content-Type`  | `application/json`                 |

### Parameters
When `id` is omitted, a new profile is created. In this case all other arguments are required. When `id` is provided, the profile with the given ID is updated. \
The `name` field is ignored when updating a profile.

| Key                 | Type     | Required | Description                                                           |
|---------------------|----------|----------|-----------------------------------------------------------------------|
| `id`                | `int`    | `false`  | The ID of the profile to update                                       |
| `name`              | `String` | `false`  | A unique username                                                     |
| `displayName`       | `String` | `false`  | The display name of the user. If omitted, name is used                |
| `profilePictureUrl` | `String` | `false`  | The profile pricuture url. Optional in all cases                      |
| `primaryEmail`      | `String` | `false`  | Primary email. If `X-User-Email` header is set its value will be used |

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
    "name": "marvin",
    "displayName": "MarfienGamerXX",
    "profilePictureUrl": "https://fuck-u.com",
    "primaryEmail": "mail@123.xom"
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
    "name": "marvin",
    "displayName": "MarfienGamerXX",
    "profilePictureUrl": "https://fuck-u.com",
    "primaryEmail": "mail@123.xom"
  }
}
</pre>
      </td>
    </tr>
    <tr>
      <td>400</td>
      <td>Missing arguments</td>
      <td>
        <pre lang="json">
{
  "success": false,
  "status": 400,
  "message": "Profile name must not be null or empty"
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
    <tr>
      <td>403</td>
      <td>Username already exists</td>
      <td>
        _Not implemented yet_
      </td>
    </tr>
  </tbody>
</table>


### Example Request
```shell
curl -X 'PUT' \
  'http://localhost:8080/api/v1/profiles' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "name": "Marvin",
  "displayName": "MarfienGamerXX",
  "profilePictureUrl": "https://fuck-u.com",
  "primaryEmail": "string"
}'
```

## DELETE `/api/v1/profiles/:id/`

Deletes a profile.

### Headers
_None_

### Parameters
| Key  | Type  | Required | Description                     |
|------|-------|----------|---------------------------------|
| `id` | `int` | `true`   | The ID of the profile to update |

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
      <td>Deleted</td>
      <td>
        <pre lang="json">
{
  "success": true,
  "status": 200,
  "data": {
    "id": 1,
    "name": "marvin",
    "displayName": "MarfienGamerXX",
    "profilePictureUrl": "https://fuck-u.com",
    "primaryEmail": "mail@123.xom"
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
  "message": "Profile not found"
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
  </tbody>
</table>


### Example Request
```shell
curl -X 'DELETE' \
  'http://localhost:8080/api/v1/profiles/1' \
  -H 'accept: */*'
```

## PUT `/api/v1/profiles/:id/contact-information`

Updates contact info of a profile.

### Headers
_None_

### Parameters
| Key  | Type                                          | Required | Description                                        |
|------|-----------------------------------------------|----------|----------------------------------------------------|
| `id` | `int`                                         | `true`   | The ID of the profile to update                    |
| `[]` | `Array<id: int, type: String, value: String>` | `true`   | The updated contact information. Id can be omitted |

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
    "name": "marvin",
    "displayName": "MarfienGamerXX",
    "profilePictureUrl": "https://fuck-u.com",
    "primaryEmail": "mail@123.xom"
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
  "message": "Profile not found"
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
  </tbody>
</table>


### Example Request
```shell
curl -X 'DELETE' \
  'http://localhost:8080/api/v1/profiles/1' \
  -H 'accept: */*'
```

## GET `/api/v1/profiles/:id/contact-information`

Get all contact information about a profile.

### Headers
_None_

### Parameters
| Key           | Type  | Required | Description                     |
|---------------|-------|----------|---------------------------------|
| `id`          | `int` | `true`   | The ID of the profile to update |

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
      "profileId": 1,
      "type": "E-Mail",
      "value": "test@123.com"
    },
    {
      "id": 6,
      "profileId": 1,
      "type": "Tel",
      "value": "123"
    }
  ]
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
  "message": "Profile not found"
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
  </tbody>
</table>


### Example Request
```shell
curl -X 'GET' \
  'http://localhost:8080/api/v1/profiles/1/contact-information' \
  -H 'accept: */*'
```


