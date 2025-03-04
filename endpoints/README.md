# Endpoint specification

Files in this directory are used to specify the endpoints of the API.
Each file should contain a description of the endpoint, the HTTP method, the URL, the request body, the response body, and the response status code.

Currently, the API has the following endpoints:
- [/api/v1/profiles](profiles.md)
- [/api/v1/restaurants](restaurants.md)
- [/api/v1/sessions](sessions.md)

In addition to the documented endpoints, each service provides a swagger ui at `/api/v1/<server>/_/swagger` that can be used to interact with the API.