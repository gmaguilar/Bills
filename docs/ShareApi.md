# ShareApi

All URIs are relative to *http://localhost:8081*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getpartaker**](ShareApi.md#getpartaker) | **GET** /bill/{billId}/partaker | Get the list of partaker for a specific bill |
| [**shareBill**](ShareApi.md#shareBill) | **POST** /bill/{billId}/share | Share a bill with other users |


<a id="getpartaker"></a>
# **getpartaker**
> List&lt;PartakerBudget&gt; getpartaker(billId)

Get the list of partaker for a specific bill

Retrieve the list of users who are partaker of a specific bill, along with the quantitys they are responsible for. The billId is provided in the path parameter. The response will include the details of each partaker, including their user ID and the quantity they are responsible for contributing to the bill. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The billId provided in the path must correspond to an existing bill in the system. If the billId is invalid or does not exist, a 404 Not Found error will be returned. The billId provided in the path must be for the authenticated user. If the billId belongs to a different user, a 403 Forbidden error will be returned. The response will be in JSON format, and the partaker details will be structured according to the PartakerBudget schema defined in the components section of the API documentation. The user can use this endpoint to view the list of partaker for a specific bill, including their contributions, and to verify that the bill has been shared correctly with the intended users.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.ShareApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    ShareApi apiInstance = new ShareApi(defaultClient);
    UUID billId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | The ID of the bill.
    try {
      List<PartakerBudget> result = apiInstance.getpartaker(billId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling ShareApi#getpartaker");
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
| **billId** | **UUID**| The ID of the bill. | |

### Return type

[**List&lt;PartakerBudget&gt;**](PartakerBudget.md)

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

<a id="shareBill"></a>
# **shareBill**
> Bill shareBill(billId, shareBillRequest)

Share a bill with other users

Share a bill with other user by providing its userId and the corresponding quantitys it should contribute. The billId is provided in the path, and the sharing details are provided in the request body. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The billId provided in the path must correspond to an existing bill in the system. If the billId is invalid or does not exist, a 404 Not Found error will be returned. The sharing details provided in the request body must be valid and complete. If the sharing details are invalid or incomplete, a 400 Bad Request error will be returned. The billId provided in the path must be for the authenticated user. If the billId belongs to a different user, a 403 Forbidden error will be returned. The user can also use this endpoint to share the bill for record-keeping purposes or to facilitate payment collection from other users. Once the bill is successfully shared, the response will include the updated details of the bill, reflecting the sharing information and the field isShared will be set to true and partaker will contain the userId

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.ShareApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    ShareApi apiInstance = new ShareApi(defaultClient);
    UUID billId = UUID.randomUUID(); // UUID | ID of the bill to share
    ShareBillRequest shareBillRequest = new ShareBillRequest(); // ShareBillRequest | 
    try {
      Bill result = apiInstance.shareBill(billId, shareBillRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling ShareApi#shareBill");
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
| **billId** | **UUID**| ID of the bill to share | |
| **shareBillRequest** | [**ShareBillRequest**](ShareBillRequest.md)|  | |

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

