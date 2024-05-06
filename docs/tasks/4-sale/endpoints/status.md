# **API Health Check Status**

This endpoint allows developers to perform real-time health checks on the API to ensure its availability and responsiveness.

## **Endpoint**

**HTTP Method:**  `GET`

```http
{REPLACE_WITH_YOUR_BASE_URL}/status
```

## **Headers**

No headers are required for this endpoint.

## **Request Code Example**

```dart linenums="1" 
import 'package:http/http.dart' as http;

void main() {
  checkApiHealth();
}

Future<void> checkApiHealth() async {
  var url = Uri.parse('http://api.example.com/status');
  var response = await http.get(url);

  if (response.statusCode == 200) {
    print('API is healthy');
  } else {
    print('Failed to check API health: ${response.statusCode}');
  }
}
```

## **Response**

The API returns a `200 OK` status code if the service is healthy and operational. If the service is down or experiencing issues, an appropriate error status code is returned.

### **Response Codes**

=== 200 OK
    The API is healthy and operational.
=== 503 Service Unavailable
    The API is down or experiencing issues.
=== 500 Internal Server Error
    An internal server error occurred.