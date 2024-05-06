# **Fetching User's Personalized Recommendations**

This endpoint allows developers to retrieve personalized recommendations for a specific user based on their preferences and behavior. Developers can specify optional query parameters to filter recommendations by category, brand, or price range.

## **Endpoint**

**HTTP Method:** `GET`

```http linenums="1" title="Personalized Recommendations Endpoint"  
{REPLACE_WITH_YOUR_BASE_URL}/users/{user_id}/recommendations
```

### **Path Parameters**

| **Parameter Name** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `user_id` | string | The unique identifier of the user for whom recommendations are requested. |

## **Headers**

| **Parameter** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `Authorization` | string | Bearer token to authenticate the API request. |
| `Content-Type` | string | The format of the request body. **Value:** `application/json` |

## **Query Parameters**

| Parameter Name | Type | Description |
|:--------------------------|:------|:-------------|
| `category` | string | Filter recommendations by category. |
| `brand` | string | Filter recommendations by brand. |
| `price_range` | string | Filter recommendations by price range. |
| `limit` | integer | The maximum number of recommendations to return. **default: 10** |
| `page` | integer | The page number for paginated results. **default: 1** |

## **Request Code Example**

!!! note "The following example is in Dart using the `http` package."

```dart linenums="1" title="Fetching Recommendations Example"
import 'dart:convert';
import 'package:http/http.dart' as http;
void main() async {
 String accessToken = 'your_access_token_here';

  var url = Uri.parse('http://api.example.com/users/$userId/recommendations?category=$category');
  var response = await http.get(
    url,
    headers: <String, String>{
      'Authorization': 'Bearer $accessToken',
    },
  );

  if (response.statusCode == 200) {
    var data = jsonDecode(response.body);
    print(data);
  } else {
    print('Failed to load recommendations: ${response.statusCode}');
  }
}
```

## **Response**

!!! tip "Implement Cache Mechanism"
    To optimize performance, consider implementing a caching mechanism to store and retrieve recommendations efficiently.

A JSON object containing a list of recommended items tailored to the user's preferences.

| **Field** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `user_id` | string | The unique identifier of the user. |
| `recommendations` | array | An array of recommended items. |

### **`recommendations` Item Fields**

| **Field** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `item_id` | string | The unique identifier of the recommended item. |
| `name` | string | The name of the recommended item. |
| `category` | string | The category of the recommended item. |
| `brand` | string | The brand of the recommended item. |
| `price` | float | The price of the recommended item. |


=== " Success Response Example"

```json linenums="1"
{
  "user_id": "123",
  "recommendations": [
    {
      "item_id": "12345",
      "name": "Product A",
      "category": "Electronics",
      "brand": "Brand X",
      "price": 99.99
    },
    {
      "item_id": "67890",
      "name": "Product B",
      "category": "Clothing",
      "brand": "Brand Y",
      "price": 49.99
    }
  ]
}
```

### **Error Responses**

=== "User Not Found"

    ```json
    {
    "error": "404",
    "message": "User not found."
    }
    ```
=== "Invalid Parameters"

    ```json
    {
    "error": "400",
    "message": "Invalid query parameters."
    }
    ```
=== "Internal Server Error"

    ```json
    {
    "error": "500",
    "message": "Internal server error. Please try again later."
    }
    ```
