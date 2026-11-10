# ExportApi

All URIs are relative to *http://localhost:8081*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**exportBillList**](ExportApi.md#exportBillList) | **GET** /bill/export | Export bill list |


<a id="exportBillList"></a>
# **exportBillList**
> String exportBillList(userId, initialDate, finalDate, status, paymentMethod, categoryId)

Export bill list

Export the list of bills based on various criteria such as user ID, category ID, status, payment method, date range, quantity range, text search, and active status. The exported data will be in a format suitable for further analysis or record-keeping. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The response will include the exported bill data in a structured format, which can be downloaded or processed as needed. The user can combine multiple filters to narrow down the results. If no bills match the provided filters, an empty export will be returned. The date filters (initialDate and finalDate) should be provided in the format DD-MM-YYYY HH:MM:SS. If only one date is provided, the filter will apply from that date to the current date or from the earliest bill date to that date, respectively. The user can also filter bills by category ID, which will return the corresponding code for the category in the response. If no category ID is provided, this filter will be ignored. The category ID and user ID filters should correspond to existing categories and users in the system. If invalid IDs are provided, a 400 Bad Request error will be returned. The status and payment method filters should be one of the allowed values defined in the StatusBill and paymentMethod schemas, respectively. If invalid values are provided, a 400 Bad Request error will be returned. The response will be paginated if the number of bills exceeds a certain threshold, and the user can navigate through the pages using query parameters for page number and page size. The list of bills must be for the authenticated user. If the user ID provided in the query does not match the authenticated user&#39;s ID, a 403 Forbidden error will be returned.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.ExportApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    ExportApi apiInstance = new ExportApi(defaultClient);
    UUID userId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | 
    OffsetDateTime initialDate = OffsetDateTime.parse("2026-10-24T00:00Z"); // OffsetDateTime | 
    OffsetDateTime finalDate = OffsetDateTime.parse("2026-10-24T00:00Z"); // OffsetDateTime | 
    StatusBill status = StatusBill.fromValue("PENDIENTE"); // StatusBill | 
    PaymentMethod paymentMethod = PaymentMethod.fromValue("EFECTIVO"); // PaymentMethod | 
    UUID categoryId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | ID of the category to filter bills by. The user will receive the code corresponding to the category in the response.
    try {
      String result = apiInstance.exportBillList(userId, initialDate, finalDate, status, paymentMethod, categoryId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling ExportApi#exportBillList");
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
| **initialDate** | **OffsetDateTime**|  | [optional] |
| **finalDate** | **OffsetDateTime**|  | [optional] |
| **status** | [**StatusBill**](.md)|  | [optional] [enum: PENDIENTE, PAGADO, CANCELADO, RECLAMADO, DEVUELTO] |
| **paymentMethod** | [**PaymentMethod**](.md)|  | [optional] [enum: EFECTIVO, TARJETA, BIZUM, TRANSFERENCIA, OTRO] |
| **categoryId** | **UUID**| ID of the category to filter bills by. The user will receive the code corresponding to the category in the response. | [optional] |

### Return type

**String**

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: text/csv, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet, application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successful operation. |  -  |
| **400** | Invalid search query. The provided search query is invalid or malformed. |  -  |
| **401** | Unauthorized. The user is not authenticated. |  -  |
| **403** | Forbidden. The user does not have permission to access this resource. |  -  |
| **500** | Internal server error. An unexpected error occurred on the server. |  -  |
| **503** | Service unavailable. The server is currently unable to handle the request due to temporary overload or maintenance. |  -  |

