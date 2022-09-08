# ModelApi

All URIs are relative to **

Method | HTTP request | Description
------------- | ------------- | -------------
[**createEntityModel**](ModelApi.md#createEntityModel) | **POST** /registry/entity/model/create | Create Item
[**deleteEntityModel**](ModelApi.md#deleteEntityModel) | **DELETE** /registry/entity/model/delete | Delete Item
[**fetchEntityModel**](ModelApi.md#fetchEntityModel) | **GET** /registry/entity/model/fetch | Fetch Item
[**listEntityModel**](ModelApi.md#listEntityModel) | **GET** /registry/entity/model/list | List Items
[**schemaEntityModel**](ModelApi.md#schemaEntityModel) | **GET** /registry/entity/model/schema | Get Schema
[**seedEntityModel**](ModelApi.md#seedEntityModel) | **POST** /registry/entity/model/seed | Seed Item
[**uiSchemaEntityModel**](ModelApi.md#uiSchemaEntityModel) | **GET** /registry/entity/model/ui_schema | Get Ui Schema
[**updateEntityModel**](ModelApi.md#updateEntityModel) | **PUT** /registry/entity/model/update | Update Item
[**validateEntityModel**](ModelApi.md#validateEntityModel) | **POST** /registry/entity/model/validate | Validate



## createEntityModel

Create Item

create_item
POSTs a new item to the registry of the given item type. 
The item does not need to include an id or creation time 
as these will be automatically generated during creation.

Responds with the successfully created item.

If you want to seed an identity without providing full information,
you can use the seed endpoint and then use the update endpoint later.

Arguments
----------
item : item_model_type
    The item you want to create.

Returns
-------
 : GenericCreateResponse
    The create response which will include a status and the item 
    created (if it was successful).

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh createEntityModel
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **modelDomainInfo** | [**ModelDomainInfo**](ModelDomainInfo.md) |  |

### Return type

[**ModelCreateResponse**](ModelCreateResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## deleteEntityModel

Delete Item

delete_item
Admin only endpoint which can be used to delete 
objects from the registry. Delete is by ID. This
endpoint will return successfully even if the object
doesn't exist in the first place.

Arguments
----------
id : str
    The handle ID of the object to delete

Returns
-------
 : StatusResponse
    Was the deletion successful - returns true even if the item 
    did not exist.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh deleteEntityModel  id=value
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **string** |  | [default to null]

### Return type

[**StatusResponse**](StatusResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## fetchEntityModel

Fetch Item

fetch_item
Fetches the item specified by the id from the 
registry. Only returns items which fit the specified
item type in this route, or if you allow with the 
seed_allowed flag, will return seed items of 
matching category and subtype.

Arguments
----------
id : str
    The handle id of the item to fetch.
seed_allowed : bool, optional
    Do you want to allow seed items to be returned, by default False

Returns
-------
 : GenericFetchResponse
    Returns a status and possibly the item.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh fetchEntityModel  id=value  seed_allowed=value
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **string** |  | [default to null]
 **seedAllowed** | **boolean** |  | [optional] [default to false]

### Return type

[**ModelFetchResponse**](ModelFetchResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## listEntityModel

List Items

list_items
Lists all items of the specified type (by route). Sorts items 
into parsable complete entities (i.e. normal entities), parsable 
seed items (i.e. incomplete), and completely unparsable entities. 

If there are any unparsable entities, the success field of the return 
status will be False, however the items will still be provided. 

Arguments
----------

Returns
-------
 : GenericListResponse
    The list of items, sorted complete, seed and unparsable, as well 
    as counts for each type.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh listEntityModel  record_type=value
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **recordType** | [**QueryRecordTypes**](.md) |  | [optional] [default to null]

### Return type

[**ModelListResponse**](ModelListResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## schemaEntityModel

Get Schema

get_schema
Returns the auto generated pydantic model 
json schema. 

This method uses only the domain info component of
the item to ensure compliance with update and
create endpoints. 

This can be used to programmatically
generate input forms, or to validate against the 
pydantic model. You can also use the /validate 
endpoint.

Arguments
----------

Returns
-------
 : SchemaResponse
    Response with a json schema object.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh schemaEntityModel
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**JsonSchemaResponse**](JsonSchemaResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## seedEntityModel

Seed Item

seed_item
Posts a new empty item. This will mint a handle, 
set the creation time, and produce the correct 
category and sub type. This can then be updated 
later using the update endpoint.

Arguments
----------

Returns
-------
 : GenericSeedResponse
    The seed item that was created.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh seedEntityModel
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**ModelSeedResponse**](ModelSeedResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## uiSchemaEntityModel

Get Ui Schema

Returns the ui schema override provided for this model.

This is for use by the front end - enabling overriding of specific
model fields with specific components. 

Parameters
----------
protected_roles : ProtectedRole, optional
    _description_, by default Depends( read_user_protected_role_dependency)

Returns
-------
UiSchemaResponse
    A JSON style mapping of field names (possibly nested) to component overrides.

### Example

```bash
registry-api.sh uiSchemaEntityModel
```

### Parameters

This endpoint does not need any parameter.

### Return type

[**UiSchemaResponse**](UiSchemaResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: Not Applicable
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## updateEntityModel

Update Item

update_item
PUT method to apply an update to an existing item. The 
existing item can either be a complete object/item or
a seed item of matching category and subtype.

To replace an item, you provide the id of the item as
a query string alongside the domain information object
that you want to update on that item. 

Arguments
----------
id : str
    The id of the object in the registry. (Handle)
replacement_domain_info : item_domain_info_type
    The new domain specific information for that record.

Returns
-------
 : StatusResponse
    Was the update successful?

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh updateEntityModel  id=value
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **id** | **string** |  | [default to null]
 **modelDomainInfo** | [**ModelDomainInfo**](ModelDomainInfo.md) |  |

### Return type

[**StatusResponse**](StatusResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)


## validateEntityModel

Validate

validate
Validates the given item body input. If this method
responds with a success, then a create_item call 
with this input should succeed. Validates in two stages
1) ensures that the pydantic model can parse your input -
if this fails, you will receive a 422 error 2) ensures
that the provided item category and subtype are correct.

Arguments
----------
item : item_model_type
    The item which you want to validate

Returns
-------
 : StatusResponse
    Success or failure object.

See Also (optional)
--------

Examples (optional)
--------

### Example

```bash
registry-api.sh validateEntityModel
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **modelDomainInfo** | [**ModelDomainInfo**](ModelDomainInfo.md) |  |

### Return type

[**StatusResponse**](StatusResponse.md)

### Authorization

[OAuth2PasswordBearer](../README.md#OAuth2PasswordBearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

