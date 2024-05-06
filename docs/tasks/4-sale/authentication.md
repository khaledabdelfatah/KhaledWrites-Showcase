# **Authentication 🔒**

The Z Recommendation Engine API uses token-based authentication to secure access to its endpoints. Developers must obtain an access token to authenticate their requests and access the API resources. This section provides an overview of the authentication process, including obtaining and using access tokens.

## **Authentication Flow**

The authentication flow for the Z Recommendation Engine API involves the following steps:

1. **Request Access Token:** Developers must request an access token by providing their client ID and client secret to the authentication server.

2. **Receive Access Token:** Upon successful authentication, the server issues an access token that developers can use to authenticate their API requests.

3. **Include Access Token:** Developers must include the access token in the `Authorization` header of their API requests to authenticate and authorize access to the API resources.

## **Access Token Request**

To request an access token, developers must send a `POST` request to the authentication server's token endpoint with the following parameters:

### **API Endpoint**

**HTTP Method:** `POST`

```http linenums="1"
{REPLACE_WITH_YOUR_BASE_URL}/auth/token
```

### **Headers**

| Key           | Value                |
|---------------|----------------------|
| `Content-Type` | `application/json`   |

### **Request Body**

The request body must include the following parameters:

| Field         | Description                                      |
|---------------|--------------------------------------------------|
| `client_id`   | The client ID provided by the API administrator
| `client_secret` | The client secret provided by the API administrator


#### **Request Code Example**

```dart linenums="1"
Future<void> refreshToken(String refreshToken) async {
  var response = await http.post(
    Uri.parse('http://auth.example.com/token'),
    body: {
      'grant_type': 'refresh_token',
      'refresh_token': refreshToken,
      'client_id': 'your_client_id',
      'client_secret': 'your_client_secret',
    },
  );

  if (response.statusCode == 200) {
    var newAccessToken = jsonDecode(response.body)['access_token'];
    print('New Access Token: $newAccessToken');
  } else {
    print('Failed to refresh token: ${response.statusCode}');
  }
}
```

 
## **Access Token Response**

Upon successful authentication, the server responds with an access token in the following format:


The response includes the following fields:

| Field         | Description                                      |
|---------------|------------------------------------------------
| `access_token` | The access token used to authenticate requests. |
| `token_type`   | The type of token issued (e.g., `Bearer`).       |
| `expires_in`   | The token's expiration time in seconds.         |

### **Response Example**

```json
{
  "access_token": "YOUR_ACCESS_TOKEN",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

### **Error Responses**

=== "404 Not Found"

    ```json
    {
    "error": "invalid_client",
    "error_description": "Client not found."
    }
    ```

=== "401 Unauthorized"

    ```json
    {
    "error": "invalid_client",
    "error_description": "Invalid client credentials."
    }
    ```

=== "500 Internal Server Error"

    ```json
    {
    "error": "server_error",
    "error_description": "An internal server error occurred."
    }
    ```