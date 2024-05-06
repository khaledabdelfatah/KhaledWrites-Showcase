# **Configure Recommendation Algorithms**

This endpoint allows developers to configure recommendation algorithms by adjusting parameters such as weighting factors and collaborative filtering methods. The configuration is performed using a PUT request with a JSON body.


## **Endpoint**

**HTTP Method:**  `PUT`

```http linenums="1" title="Configure Recommendation Algorithm Endpoint"
{REPLACE_WITH_YOUR_BASE_URL}/algorithms/{algorithm_id}/configure
```

### **Path Parameters**

| **Parameter Name** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `algorithm_id` | string | The unique identifier of the recommendation algorithm to configure. |

## **Headers**

| **Parameter** | **Type** | **Description** |
|:--------------------------|:------|:
| `Authorization` | string | Bearer token to authenticate the API request. |
| `Content-Type` | string | The format of the request body. **Value:** `application/json` |

## **Request Body**

| **Parameter Name** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `weighting_factors` | object | The weighting factors for the algorithm. |
| `collaborative_filtering` | object | The collaborative filtering method to use. |

### **Request Code Example**

```dart linenums="1" 
import 'dart:convert';
import 'package:http/http.dart' as http;

void main() {
  String accessToken = 'your_access_token_here';
  String algorithmId = 'xyz123';

  configureAlgorithm(
    algorithmId,
    {
      'weighting_factor': 0.8,
      'collaborative_filtering_method': 'matrix_factorization'
    },
    accessToken,
  );
}

Future<void> configureAlgorithm(String algorithmId, Map<String, dynamic> configData, String accessToken) async {
  var url = Uri.parse('http://api.example.com/algorithms/$algorithmId/configure');
  var response = await http.put(
    url,
    headers: <String, String>{
      'Authorization': 'Bearer $accessToken',
      'Content-Type': 'application/json'
    },
    body: jsonEncode(configData),
  );

  if (response.statusCode == 200) {
    print('Algorithm configured successfully');
  } else {
    print('Failed to configure algorithm: ${response.statusCode}');
  }
}
```

## **Response**

The response will indicate whether the algorithm configuration was successful or not.

=== "200"
    ```json
    {
        "message": "Algorithm configured successfully"
    }
    ```
=== "400"
    ```json
    {
        "message": "Failed to configure algorithm"
    }
    ```
=== "401"
    ```json
    {
        "message": "Unauthorized"
    }
    ```
=== "404"
    ```json
    {
        "message": "Algorithm not found"
    }
    ```
=== "500"
    ```json
    {
        "message": "Internal server error"
    }
    ```
