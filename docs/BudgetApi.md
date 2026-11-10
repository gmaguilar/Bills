# BudgetApi

All URIs are relative to *http://localhost:8081*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getBudget**](BudgetApi.md#getBudget) | **GET** /bill/{userId}/budget | Get available budget |


<a id="getBudget"></a>
# **getBudget**
> Budget getBudget(userId)

Get available budget

Retrieve the available budget for a specific user. The user ID is provided in the path parameter. The response will include the total budget, the quantity wasted, and the available budget for the user. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The user ID provided in the path must correspond to an existing user in the system. If the user ID is invalid or does not exist, a 404 Not Found error will be returned. The response will be in JSON format, and the budget details will be structured according to the budget schema defined in the components section of the API documentation. The user can use this endpoint to view their available budget and track their spending against their allocated budget. The result will be the difference between the total budget and the quantity wasted, representing the available budget for the user.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.BudgetApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    BudgetApi apiInstance = new BudgetApi(defaultClient);
    UUID userId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | 
    try {
      Budget result = apiInstance.getBudget(userId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling BudgetApi#getBudget");
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
| **userId** | **UUID**|  | |

### Return type

[**Budget**](Budget.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successful operation. |  -  |
| **400** | Invalid search query. The provided search query is invalid or malformed. |  -  |
| **401** | Unauthorized. The user is not authenticated. |  -  |
| **403** | Forbidden. The user does not have permission to access this resource. |  -  |
| **500** | Internal server error. An unexpected error occurred on the server. |  -  |
| **503** | Service unavailable. The server is currently unable to handle the request due to temporary overload or maintenance. |  -  |

