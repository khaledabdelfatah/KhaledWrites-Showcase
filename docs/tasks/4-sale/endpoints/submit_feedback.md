# **Send Feedback on a Recommendation**

This endpoint allows users to provide feedback on recommendations through upvote/downvote actions. Users can optionally provide a reason for their feedback via a POST request with a JSON body.

## **Endpoint**

**HTTP Method:** `POST`

```http linenums="1" title="Feedback on Recommendation Endpoint"
{REPLACE_WITH_YOUR_BASE_URL}/feedback
```

### **Headers**

| **Parameter** | **Type** | **Description** |
|:--------------------------|:------|:
| `Authorization` | string | Bearer token to authenticate the API request. |
| `Content-Type` | string | The format of the request body. **Value:** `application/json` |

### **Request Body**

| **Parameter Name**| **Type** | **Description** |
|:--------------------------|:------|:-------------|
| `recommendation_id` | string | The unique identifier of the recommendation for which feedback is provided. |
| `feedback` | string | The user's feedback on the recommendation where `upvote` indicates a positive feedback and `downvote` indicates a negative feedback. |
| `reason` | string | The reason for the user's feedback. (**Optional**) |

### **Request Code Example**

!!! note "The following example is in Dart using the `http` package."

```dart linenums="1" title="Sending Feedback Example"
import 'dart:convert';
import 'package:http/http.dart' as http;

void main() {
  sendFeedback('123', 'upvote', 'Great recommendation!');
}

Future<void> sendFeedback(String recommendationId, String feedback, String reason) async {
  String accessToken = 'your_access_token_here';
  var feedbackData = {
    'recommendation_id': recommendationId,
    'feedback': feedback,
    'reason': reason
  };

  var url = Uri.parse('http://api.example.com/feedback');
  var response = await http.post(
    url,
    headers: <String, String>{
      'Authorization': 'Bearer $accessToken',
      'Content-Type': 'application/json'
    },
    body: jsonEncode(feedbackData),
  );

  if (response.statusCode == 200) {
    print('Feedback submitted successfully');
  } else {
    print('Failed to submit feedback: ${response.statusCode}');
  }
}
```

### **Response**

The response will indicate whether the feedback was successfully submitted or if there was an error in the request. The status code `200` indicates a successful submission.

```json
{
  "message": "Feedback submitted successfully"
}
```

### **Error Response**

=== "Missing Required Fields"
    If the required fields are missing in the request body, the API will return an error response with a status code `400`.

    ```json
    {
      "error": "400", 
      "message": "Missing required fields: recommendation_id, feedback"
    }
    ```
=== "Invalid Feedback Value"
    If the `feedback` value is not valid (i.e., not `upvote` or `downvote`), the API will return an error response with a status code `400`.

    ```json
    {
      "error": "400", 
      "message": "Invalid feedback value. Please provide 'upvote' or 'downvote'."
    }
    ```
=== "Internal Server Error"
    If there is an issue on the server side, the API will return an error response with a status code `500`.

    ```json
    {
      "error": "500", 
      "message": "Internal Server Error. Please try again later."
    }
    ```        