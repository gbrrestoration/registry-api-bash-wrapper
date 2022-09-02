# GeneralRegistryApi

All URIs are relative to **

Method | HTTP request | Description
------------- | ------------- | -------------
[**fetch**](GeneralRegistryApi.md#fetch) | **GET** /registry/general/fetch | Fetch Item
[**list**](GeneralRegistryApi.md#list) | **POST** /registry/general/list | List Items



## fetch

Fetch Item

### Example

```bash
registry-api.sh fetch  id=value
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **string** |  | [default to null]

### Return type

[**UntypedFetchResponse**](UntypedFetchResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## list

List Items

list_items
Lists all items in the registry based on the provided query filter.
You can use the query_filter.record_type field to specify what kind of 
records can be returned. By default, only COMPLETE record (non seed 
records) are returned.
The items in this method are not parsed in any way.

Arguments
----------

Returns
-------
 : UnparsedListResponse
 The list of items and a total count, no parsing.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh list
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **queryFilter** | [**QueryFilter**](QueryFilter.md) |  |

### Return type

[**UnparsedListResponse**](UnparsedListResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

