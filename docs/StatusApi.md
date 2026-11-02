# StatusApi

All URIs are relative to *http://localhost:8081*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**changeStatus**](StatusApi.md#changeStatus) | **PATCH** /bill/{billId}/status | Change the status of a bill |


<a id="changeStatus"></a>
# **changeStatus**
> Bill changeStatus(billId, changeStatusRequest)

Change the status of a bill

Update the status of an existing bill. The billId is provided in the path, and the new status is provided in the request body. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The billId provided in the path must correspond to an existing bill in the system. If the billId is invalid or does not exist, a 404 Not Found error will be returned. The new status provided in the request body must be one of the allowed values defined in the StatusBill schema. If an invalid status is provided, a 400 Bad Request error will be returned. The billId provided in the path must be for the authenticated user. If the billId belongs to a different user, a 403 Forbidden error will be returned. The endpoint will return the details of the updated bill, including its unique ID, user ID, quantity, description, category ID, status, payment method, shared status, creation and modification timestamps, and active status. The user can use this endpoint to change the status of a bill, such as marking it as paid or pending, and the updated status will be reflected in subsequent queries for bills. The response will be in JSON format, and the updated bill details will be structured according to the Bill schema defined in the components section of the API documentation. The user can also use this endpoint to update the status of a bill for record-keeping purposes or to reflect changes in the bill&#39;s payment status.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.StatusApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    StatusApi apiInstance = new StatusApi(defaultClient);
    UUID billId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | 
    ChangeStatusRequest changeStatusRequest = new ChangeStatusRequest(); // ChangeStatusRequest | 
    try {
      Bill result = apiInstance.changeStatus(billId, changeStatusRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling StatusApi#changeStatus");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **billId** | **UUID**|  | |
| **changeStatusRequest** | [**ChangeStatusRequest**](ChangeStatusRequest.md)|  | |

### Return type

[**Bill**](Bill.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successful operation. |  -  |
| **400** | Invalid billId. The provided billId is invalid or malformed. |  -  |
| **401** | Unauthorized. The user is not authenticated. |  -  |
| **403** | Forbidden. The user does not have permission to access this resource. |  -  |
| **500** | Internal server error. An unexpected error occurred on the server. |  -  |
| **503** | Service unavailable. The server is currently unable to handle the request due to temporary overload or maintenance. |  -  |

