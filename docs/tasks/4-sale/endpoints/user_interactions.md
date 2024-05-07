# **Manage User Interaction Data**

This endpoint allows you to manage user interaction data, such as views, purchases, and likes, to personalize recommendations for users. You can create, update, and delete interactions using this endpoint.

## **Endpoint**

**HTTP Methods:** 

- `POST` : Create a new interaction for the user.
- `PUT` : Update an existing interaction for the user.
- `DELETE` : Delete an interaction for the user.

```http linenums="1" title="User Interaction Data Endpoint"
{REPLACE_WITH_YOUR_BASE_URL}/user-data/{user_id}/interactions
```

### **Path Parameters**

| **Parameter Name** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `user_id` | string | The unique identifier of the user for whom interactions are managed. |

### **Headers**

| **Parameter** | **Type** | **Description** |
|:--------------------------|:------|:
| `Authorization` | string | Bearer token to authenticate the API request. |
| `Content-Type` | string | The format of the request body. **Value:** `application/json` |

### **Request Body**

=== "POST Request Body"
    | **Parameter Name** | **Type** | **Description** |
    |:--------------------------|:------|:-------------|
    | `item_id` | string | The unique identifier of the item the user interacted with. |
    | `interaction_type` | string | The type of interaction (e.g., `view`, `purchase`, `like`). |
    | `timestamp` | string | The timestamp of the interaction in ISO 8601 format. |

=== "PUT Request Body"
    | **Parameter Name** | **Type** | **Description** |
    |:--------------------------|:------|:-------------|
    | `interaction_id` | string | The unique identifier of the interaction to update. |
    | `item_id` | string | The unique identifier of the item the user interacted with. |
    | `interaction_type` | string | The type of interaction (e.g., `view`, `purchase`, `like`). |
    | `timestamp` | string | The timestamp of the interaction in ISO 8601 format. |

=== "DELETE Request Body"
    | **Parameter Name** | **Type** | **Description** |
    |:--------------------------|:------|:-------------|
    | `interaction_id` | string | The unique identifier of the interaction to delete. |

### **Request Code Examples**

!!! note "The following examples are in Dart using the `http` package."

=== "Creating an Interaction (POST Request)"

    ```dart linenums="1" 
    import 'dart:convert';
    import 'package:http/http.dart' as http;

    Future<void> createInteraction(String userId, String interactionType, String itemId, String timestamp, String accessToken) async {
    var interactionData = {
        'interaction_type': interactionType,
        'item_id': itemId,
        'timestamp': timestamp
    };

    var url = Uri.parse('http://api.example.com/user-data/$userId/interactions');
    var response = await http.post(
        url,
        headers: <String, String>{
        'Authorization': 'Bearer $accessToken',
        'Content-Type': 'application/json'
        },
        body: jsonEncode(interactionData),
    );

    if (response.statusCode == 200) {
        print('Interaction created successfully');
    } else {
        print('Failed to create interaction: ${response.statusCode}');
    }
    }
    ```
=== "Updating Interaction (PUT Request)"

    ```dart linenums="1"
    import 'dart:convert';
    import 'package:http/http.dart' as http;

    Future<void> updateInteraction(String userId, String interactionId, String interactionType, String timestamp, String accessToken) async {
    var interactionData = {
    'interaction_id': interactionId,
    'interaction_type': interactionType,
    'timestamp': timestamp
    };

    var url = Uri.parse('http://api.example.com/user-data/$userId/interactions');
    var response = await http.put(
    url,
    headers: <String, String>{
        'Authorization': 'Bearer $accessToken',
        'Content-Type': 'application/json'
    },
    body: jsonEncode(interactionData),
    );

    if (response.statusCode == 200) {
    print('Interaction updated successfully');
    } else {
    print('Failed to update interaction: ${response.statusCode}');
    }
    }
    ```

=== "Deleting an Interaction (DELETE Request)"

    ```dart linenums="1"    
    import 'dart:convert';
    import 'package:http/http.dart' as http;

    Future<void> deleteInteraction(String userId, String interactionId, String accessToken) async {
    var interactionData = {
    'interaction_id': interactionId
    };

    var url = Uri.parse('http://api.example.com/user-data/$userId/interactions');
    var response = await http.delete(
    url,
    headers: <String, String>{
        'Authorization': 'Bearer $accessToken',
        'Content-Type': 'application/json'
    },
    body: jsonEncode(interactionData),
    );

    if (response.statusCode == 200) {
    print('Interaction deleted successfully');
    } else {
    print('Failed to delete interaction: ${response.statusCode}');
    }
    }
    ```

## **Response**

The response will be a status code indicating the success or failure of the request.

=== "200"
    The request was successful.
=== "400"
    The request was invalid or malformed.
=== "401"
    The request was not authorized.
=== "404"
    The requested resource was not found.
=== "500"
    An error occurred on the server.    
