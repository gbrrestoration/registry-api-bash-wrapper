# AdminApi

All URIs are relative to **

Method | HTTP request | Description
------------- | ------------- | -------------
[**registryAdminExport**](AdminApi.md#registryAdminExport) | **GET** /admin/export | Export Items
[**registryAdminImport**](AdminApi.md#registryAdminImport) | **POST** /admin/import | Import Items Parsed
[**registryAdminRestore**](AdminApi.md#registryAdminRestore) | **POST** /admin/restore_from_table | Restore From Table Parsed



## registryAdminExport

Export Items

Provides a mechanism for admins to dump the current contents of the registry
table without any validation/parsing.

Parameters
----------

Returns
-------
RegistryExportResponse
    A status response including items in the payload.

### Example

```bash
registry-api.sh registryAdminExport
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**RegistryExportResponse**](RegistryExportResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## registryAdminImport

Import Items Parsed

This admin only endpoint enables rapid restoration of items in into the
registry table. 

The import mode describes what kind of rules you want to apply about items. 

The import_request contains the import mode, and other settings described
below.

Import mode - 

ADD ONLY - will only add items - all items must be new and not exist in
current registry.

ADD_OR_OVERWRITE - will only add or overwrite existing items. This form of
import will always validate as any items are valid.

OVERWRITE_ONLY - all items must already exist in the registry, update will
be applied with the new contents.

SYNC_ADD_OR_OVERWRITE - sync mode is the same as ADD OR OVERRIDE but also
enforces that there are no items in the current table which are not in the
import items payload. If there are such items, this validation will fail -
consider using the item below.

SYNC_DELETION_ALLOWED - this will perform whatever is necessary to make the
current registry table be identical to the provided items, including
potentially deleting existing entries. USE WITH CAUTION. You must specify
allow_entry_deletion explicitly to enable deletion.

Parse items - this flag forces all items in the item payload to be parsed as
their respective models. For example, if the list includes an item with a
category/subtype but a body which doesn't parse as that type, then the
import will fail.

Allow entry deletion - this flag is only for use in the sync deletion
allowed mode, and is a secondary defense against accidental deletion. Set to
TRUE to enable deletion.

Trial mode - this is a flag which determines whether a trial mode is being
run. Trial mode will perform the entire process with the exception of
actually writing any changes. True = trial mode. False = write changes.
Default = True.

Parameters
----------
import_request : RegistryImportRequest
    The import request payload, as described above.

Returns
-------
RegistryImportResponse
    Returns an import response which includes status + statistics.

Raises
------
http_exception
    Handled exception within import logic 
HTTPException
    500 error if something else goes wrong

### Example

```bash
registry-api.sh registryAdminImport
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **registryImportRequest** | [**RegistryImportRequest**](RegistryImportRequest.md) |  |

### Return type

[**RegistryImportResponse**](RegistryImportResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## registryAdminRestore

Restore From Table Parsed

Provides an admin only mechanism for restoring the entire contents of the
table from another dynamoDB table.

NOTE the admin runtime must have AWS permissions to read from the table. If
you are running the API locally then it is likely your local runtime will
have these permissions if you are signed into AWS. However, if you are
running this against a live API, you may need to update the CDK deployment
to have read only permissions into the specified table.

This is achieved by dumping the contents of the external table, then using
the contents in the item payload to the import operation. The options
provided in the import request here are propagated into the import request.

For more information about the import options, see the /import endpoint.

Parameters
----------
import_request : RegistryRestoreRequest
    The import request settings - these will be used when propagating the
    items from the external table.
table_name : str
    The name of the external table

Returns
-------
RegistryImportResponse
    Returns information about the import, including status and statistics.

Raises
------
http_exception
    If a handled error occurs during the import operation, will raise it
HTTPException
    Otherwise a 500 error is returned with error details

### Example

```bash
registry-api.sh registryAdminRestore  table_name=value
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **tableName** | **string** |  | [default to null]
 **registryRestoreRequest** | [**RegistryRestoreRequest**](RegistryRestoreRequest.md) |  |

### Return type

[**RegistryImportResponse**](RegistryImportResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

