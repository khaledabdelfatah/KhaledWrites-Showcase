# **Fetching Similar Items**

This endpoint enables developers to retrieve a list of items similar to a specific item, along with a confidence score for each recommendation. This can help users discover related items based on their interests.

## **Endpoint**

**HTTP Method:** `GET`

```http linenums="1" title="Similar Items Endpoint"
{REPLACE_WITH_YOUR_BASE_URL}/items/{item_id}/similar
```

### **Path Parameters**

| **Parameter Name** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `item_id` | string | The unique identifier of the item for which similar items are requested. |

## **Headers**

| **Parameter** | **Type** | **Description** |
|:--------------------------|:------|:
| `Authorization` | string | Bearer token to authenticate the API request. |
| `Content-Type` | string | The format of the request body. **Value:** `application/json` |

## **Query Parameters**

| Parameter Name | Type | Description |
|:--------------------------|:------|:-------------|
| `limit` | integer | The maximum number of similar items to return. **default: 10** |
| `page` | integer | The page number for paginated results. **default: 1** |

## **Request Code Example**

!!! note "The following example is in Dart using the `http` package."

```dart linenums="1" title="Fetching Similar Items Example"
import 'dart:convert';
import 'package:http/http.dart' as http;

void main() {
  getSimilarItems('123');
}

Future<void> getSimilarItems(String itemId) async {
  String accessToken = 'your_access_token_here';

  var url = Uri.parse('http://api.example.com/items/$itemId/similar_items');
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
    print('Failed to load similar items: ${response.statusCode}');
  }
}
```

## **Response**

!!! tip "Implement Cache Mechanism"
    To optimize performance, consider implementing a caching mechanism to store and retrieve recommendations efficiently.

The API response contains an array of `items` similar to the requested item, along with a confidence score for each recommendation. each item in the array contains the following fields:

| **Field** | **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `id` | string | The unique identifier of the item. |
| `name` | string | The name of the item. |
| `price` | number | The price of the item. |
| `image_url` | string | The URL of the item's image. |
| `confidence` | number | A confidence score indicating the similarity of the item to the requested item. |

```json
{
  "items": [
    {
      "id": "456",
      "name": "Product Name",
      "price": 99.99,
      "image_url": "http://example.com/image.jpg",
      "confidence": 0.85
    },
    {
      "id": "789",
      "name": "Another Product",
      "price": 49.99,
      "image_url": "http://example.com/another.jpg",
      "confidence": 0.75
    }
  ]
}
```

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
      "message": "Item not found"
    }
    ```    
