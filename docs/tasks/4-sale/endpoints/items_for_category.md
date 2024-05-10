# **Fetching Items for Category Endpoint**

Developers can use this endpoint to get recommendations for items in a specific category. The endpoint allows specifying the number of recommendations returned, providing flexibility in customizing the recommendation list.

## **Endpoint**

**HTTP Method:** `GET`

```http linenums="1" title="Items for Category Endpoint"
{REPLACE_WITH_YOUR_BASE_URL}/categories/{category_id}/recommendations
```

### **Path Parameters**

| **Parameter Name** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `category_id` | string | The unique identifier of the category for which recommendations are requested. |

## **Headers**

| **Parameter** | **Type** | **Description** |
|:--------------------------|:------|:
| `Authorization` | string | Bearer token to authenticate the API request. |
| `Content-Type` | string | The format of the request body. **Value:** `application/json` |

## **Query Parameters**

| Parameter Name | Type | Description |
|:--------------------------|:------|:-------------|
| `limit` | integer | The maximum number of recommendations to return. **default: 10** |
| `page` | integer | The page number for paginated results. **default: 1** |

## **Request Code Example**

!!! note "The following example is in Dart using the `http` package."

```dart linenums="1" title="Fetching Items for Category Example"
import 'dart:convert';
import 'package:http/http.dart' as http;

void main() {
  getCategoryRecommendations('123');
}

Future<void> getCategoryRecommendations(String categoryId) async {
  String accessToken = 'your_access_token_here';

  var url = Uri.parse('http://api.example.com/categories/$categoryId/recommendations');
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
    print('Failed to load category recommendations: ${response.statusCode}');
  }
}
```

## **Response**

The response will be a JSON object containing the list of recommended `items` for the specified category. each item will have the following attributes:

| **Attribute** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `id` | string | The unique identifier of the item. |
| `name` | string | The name of the item. |
| `price` | float | The price of the item. |
| `category` | string | The category of the item. |
| `brand` | string | The brand of the item. |
| `image_url` | string | The URL of the item's image. |



```json linenums="1" title="Response Example"
{
  "items": [
    {
      "id": "123",
      "name": "Product Name",
      "price": 100.0,
      "category": "Category Name",
      "brand": "Brand Name",
      "image_url": "https://example.com/image.jpg"
    },
    {
      "id": "456",
      "name": "Product Name 2",
      "price": 200.0,
      "category": "Category Name",
      "brand": "Brand Name",
      "image_url": "https://example.com/image2.jpg"
    }
  ]
}
```

!!! tip "Implement Cache Mechanism"
    To optimize performance, consider implementing a caching mechanism to store and retrieve recommendations efficiently.

### **Error Responses**

=== "Unauthorized"
    ```json
    {
      "error": "401",  
      "message": "Unauthorized"
    }
    ```

=== "Not Found"
    ```json
    {
      "error": "404",  
      "message": "Category not found"
    }
    ```
