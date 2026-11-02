# BillApi

All URIs are relative to *http://localhost:8081*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**createBill**](BillApi.md#createBill) | **POST** /bill | Create a bill. |
| [**deleteBill**](BillApi.md#deleteBill) | **DELETE** /bill/{billId} | Delete a bill |
| [**getBillById**](BillApi.md#getBillById) | **GET** /bill/{billId} | Get a bill by its ID. |
| [**listBill**](BillApi.md#listBill) | **GET** /bill | List and filter bills based on various criteria. |
| [**updateBill**](BillApi.md#updateBill) | **PUT** /bill/{billId} | Update a bill |


<a id="createBill"></a>
# **createBill**
> Bill createBill(billRequest)

Create a bill.

Create a new bill with the provided details. The request body must contain the necessary information to create the bill. The categoryId must correspond to an existing category, and the paymentMethod must be one of the allowed values. The userId must be a valid user in the system. The bill will be created with a default status of \&quot;PENDIENTE\&quot; and will be marked as active. If the bill is shared, the shared field will be set to true and the partaker field will contain the userId with whom the bill is shared. The response will include the details of the created bill, including its unique ID and timestamps for creation and modification. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. Only authenticated users can create bills. The partaker field will only be populated if the bill is shared. It is requiered communication with the Category microservice to validate the categoryId provided in the bill request. When a new bill is created, the system will communicate with the User microservice to update the user&#39;s qtyWasted accordingly. To obtain the category the system will comunicate with the endpoint GET -&gt; /category

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.BillApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    BillApi apiInstance = new BillApi(defaultClient);
    BillRequest billRequest = new BillRequest(); // BillRequest | 
    try {
      Bill result = apiInstance.createBill(billRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling BillApi#createBill");
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
| **billRequest** | [**BillRequest**](BillRequest.md)|  | |

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
| **200** | Successful operation. Bill created |  -  |
| **400** | Unable to create bill. The provided bill data is invalid or incomplete. |  -  |
| **401** | Unauthorized. The user is not authenticated. |  -  |
| **403** | Forbidden. The user is authenticated but does not have permission to access the requested resource. |  -  |
| **500** | Internal server error. An unexpected error occurred on the server. |  -  |
| **503** | Service unavailable. The server is currently unable to handle the request due to temporary overload or maintenance. |  -  |

<a id="deleteBill"></a>
# **deleteBill**
> Bill deleteBill(billId)

Delete a bill

Perform a logical delete on a bill. The billId is provided in the path, and the user must be authenticated to access this endpoint. The provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The billId provided in the path must correspond to an existing bill in the system. If the billId is invalid or does not exist, a 404 Not Found error will be returned. The billId provided in the path must be for the authenticated user. If the billId belongs to a different user, a 403 Forbidden error will be returned. The response will include the details of the deleted bill, including its unique ID, user ID, quantity, description, category ID, status, payment method, shared status, creation and modification timestamps, and active status.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.BillApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    BillApi apiInstance = new BillApi(defaultClient);
    UUID billId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | 
    try {
      Bill result = apiInstance.deleteBill(billId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling BillApi#deleteBill");
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

### Return type

[**Bill**](Bill.md)

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

<a id="getBillById"></a>
# **getBillById**
> Bill getBillById(billId)

Get a bill by its ID.

Retrieve the details of a specific bill using its unique ID. The billId is provided in the path parameter. The response will include the details of the bill, including its unique ID, userId, quantity, description, categoryId, status, payment method, shared status, creation and modification timestamps, and active status. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. If the token is missing or invalid, a 401 Unauthorized error will be returned. The billId provided in the path must correspond to an existing bill in the system. If the billId is invalid or does not exist, a 404 Not Found error will be returned. The billId provided in the path must be for the authenticated user. If the billId belongs to a different user, a 403 Forbidden error will be returned. The response will be in JSON format, and the bill details will be structured according to the Bill schema defined in the components section of the API documentation. The user can use this endpoint to view the details of a specific bill, including its status and payment method, and to verify that the bill has been created and stored correctly in the system. The user can also use this endpoint to retrieve the bill details for further processing, such as updating the bill, sharing it with other users, or exporting it for record-keeping purposes. If the quantity of the bill is updated, it will also affect the user&#39;s qtyWasted accordingly.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.BillApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    BillApi apiInstance = new BillApi(defaultClient);
    UUID billId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | 
    try {
      Bill result = apiInstance.getBillById(billId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling BillApi#getBillById");
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

### Return type

[**Bill**](Bill.md)

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

<a id="listBill"></a>
# **listBill**
> List&lt;Bill&gt; listBill(userId, categoryId, status, paymentMethod, initialDate, finalDate, quantityMin, quantityMax, text, partakerId, isActive)

List and filter bills based on various criteria.

Retrieve a list of bills, optionally filtered by userId, categoryId, status, paymentMethod, dates, quantity, and active status. If the user does not provide any filters, all its bills will be returned. The response will include the details of each bill, including its unique ID, user ID, quantity, description, category ID, status, payment method, shared status, creation and modification timestamps, and active status. The user can combine multiple filters to narrow down the results. If no bills match the provided filters, an empty array will be returned. The user must be authenticated to access this endpoint, and the provided bearer token must be valid. The date filters (initialDate and finalDate) should be provided in the format DD-MM-YYYY HH:MM:SS. If only one date is provided, this date will be used as both the start and end date for filtering. The quantity filter should be provided as numeric values. The isActive filter allows the user to retrieve only active bills (true) or only inactive bills (false). If not provided, the default behavior is to return only active bills. The user can also filter bills by categoryId, which will return the corresponding code for the category in the response. If no categoryId is provided, this filter will be ignored. It is necessary comunication with the Category microservice to validate the categoryId provided in the bill request. The categoryId should correspond to existing categories in the system. If invalid IDs are provided, a 400 Bad Request error will be returned. The status and payment method filters should be one of the allowed values defined in the StatusBill and paymentMethod schemas, respectively. If invalid values are provided, a 400 Bad Request error will be returned. The list of bills must be for the authenticated user. If the user ID provided in the query does not match the authenticated user&#39;s ID, a 403 Forbidden error will be returned.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.BillApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    BillApi apiInstance = new BillApi(defaultClient);
    UUID userId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | ID of the user to filter bills by. It will only return bills belonging to this user.
    UUID categoryId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | ID of the category to filter bills by. The user will receive the code corresponding to the category in the response.
    StatusBill status = StatusBill.fromValue("PENDIENTE"); // StatusBill | Status of the bill to filter by.
    PaymentMethod paymentMethod = PaymentMethod.fromValue("EFECTIVO"); // PaymentMethod | Payment method of the bill to filter by.
    OffsetDateTime initialDate = OffsetDateTime.parse("2026-10-24T00:00Z"); // OffsetDateTime | Initial date to filter bills from (inclusive). The format should be DD-MM-YYYY HH:MM:SS. If not provided, the filter will start from the earliest bill date.
    OffsetDateTime finalDate = OffsetDateTime.parse("2026-10-24T00:00Z"); // OffsetDateTime | Final date to filter bills until (inclusive). The format should be DD-MM-YYYY HH:MM:SS. If not provided, the filter will include all bills up to the current date.
    Double quantityMin = 1.5D; // Double | Minimum quantity to filter bills by.
    Double quantityMax = 100.0D; // Double | Maximum quantity to filter bills by.
    String text = "Dinner with friends"; // String | Text to filter bills by.
    UUID partakerId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | ID of the partaker to filter bills by. The user will receive the code corresponding to the partaker in the response.
    Boolean isActive = true; // Boolean | Filter bills by their active status.
    try {
      List<Bill> result = apiInstance.listBill(userId, categoryId, status, paymentMethod, initialDate, finalDate, quantityMin, quantityMax, text, partakerId, isActive);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling BillApi#listBill");
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
| **userId** | **UUID**| ID of the user to filter bills by. It will only return bills belonging to this user. | [optional] |
| **categoryId** | **UUID**| ID of the category to filter bills by. The user will receive the code corresponding to the category in the response. | [optional] |
| **status** | [**StatusBill**](.md)| Status of the bill to filter by. | [optional] [enum: PENDIENTE, PAGADO, CANCELADO, RECLAMADO, DEVUELTO] |
| **paymentMethod** | [**PaymentMethod**](.md)| Payment method of the bill to filter by. | [optional] [enum: EFECTIVO, TARJETA, BIZUM, TRANSFERENCIA, OTRO] |
| **initialDate** | **OffsetDateTime**| Initial date to filter bills from (inclusive). The format should be DD-MM-YYYY HH:MM:SS. If not provided, the filter will start from the earliest bill date. | [optional] |
| **finalDate** | **OffsetDateTime**| Final date to filter bills until (inclusive). The format should be DD-MM-YYYY HH:MM:SS. If not provided, the filter will include all bills up to the current date. | [optional] |
| **quantityMin** | **Double**| Minimum quantity to filter bills by. | [optional] |
| **quantityMax** | **Double**| Maximum quantity to filter bills by. | [optional] |
| **text** | **String**| Text to filter bills by. | [optional] |
| **partakerId** | **UUID**| ID of the partaker to filter bills by. The user will receive the code corresponding to the partaker in the response. | [optional] |
| **isActive** | **Boolean**| Filter bills by their active status. | [optional] [default to true] |

### Return type

[**List&lt;Bill&gt;**](Bill.md)

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

<a id="updateBill"></a>
# **updateBill**
> Bill updateBill(billId, billRequest)

Update a bill

Update the details of an existing bill. The billId is provided in the path, and the updated bill data is provided in the request body. The user must be authenticated to access this endpoint. The billId provided in the path must correspond to an existing bill in the system. If the billId is invalid or does not exist, a 404 Not Found error will be returned. The updated bill data provided in the request body must be valid and complete. If the updated data is invalid or incomplete, a 400 Bad Request error will be returned. The user can update the bill&#39;s, quantity, description, categoryId y paymentMethod. The response will include the details of the updated bill, including its unique ID and timestamps for creation and modification. The user can use this endpoint to correct any errors in the bill data, change the status of the bill, or update the payment method or category as needed. The updated bill will be saved in the system and will be reflected in subsequent queries for bills. The response will be in JSON format, and the updated bill details will be structured according to the Bill schema defined in the components section of the API documentation. The billId provided in the path must be for the authenticated user. If the billId belongs to a different user, a 403 Forbidden error will be returned. It is necessary communications with Category service to ensure the categoryId provided in the bill exists and is valid. If the categoryId is invalid or does not exist, a 400 Bad Request error will be returned. To obtain the category details, the system will communicate with the Category service using the GET -&gt; /category/{categoryId} endpoint.

### Example
```java
// Import classes:
import org.openapitools.client.ApiClient;
import org.openapitools.client.ApiException;
import org.openapitools.client.Configuration;
import org.openapitools.client.models.*;
import org.openapitools.client.api.BillApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("http://localhost:8081");

    BillApi apiInstance = new BillApi(defaultClient);
    UUID billId = UUID.fromString("123e4567-e89b-12d3-a456-426614174000"); // UUID | 
    BillRequest billRequest = new BillRequest(); // BillRequest | 
    try {
      Bill result = apiInstance.updateBill(billId, billRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling BillApi#updateBill");
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
| **billRequest** | [**BillRequest**](BillRequest.md)|  | |

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
| **400** | Invalid search query. The provided search query is invalid or malformed. |  -  |
| **401** | Unauthorized. The user is not authenticated. |  -  |
| **403** | Forbidden. The user does not have permission to access this resource. |  -  |
| **500** | Internal server error. An unexpected error occurred on the server. |  -  |
| **503** | Service unavailable. The server is currently unable to handle the request due to temporary overload or maintenance. |  -  |

