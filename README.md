# FastAPI Bash client

## Overview

This is a Bash client script for accessing FastAPI service.

The script uses cURL underneath for making all REST calls.

## Usage

```shell
# Make sure the script has executable rights
$ chmod u+x registry-api.sh

# Print the list of operations available on the service
$ ./registry-api.sh -h

# Print the service description
$ ./registry-api.sh --about

# Print detailed information about specific operation
$ ./registry-api.sh <operationId> -h

# Make GET request
./registry-api.sh --host http://<hostname>:<port> --accept xml <operationId> <queryParam1>=<value1> <header_key1>:<header_value2>

# Make GET request using arbitrary curl options (must be passed before <operationId>) to an SSL service using username:password
registry-api.sh -k -sS --tlsv1.2 --host https://<hostname> -u <user>:<password> --accept xml <operationId> <queryParam1>=<value1> <header_key1>:<header_value2>

# Make POST request
$ echo '<body_content>' | registry-api.sh --host <hostname> --content-type json <operationId> -

# Make POST request with simple JSON content, e.g.:
# {
#   "key1": "value1",
#   "key2": "value2",
#   "key3": 23
# }
$ echo '<body_content>' | registry-api.sh --host <hostname> --content-type json <operationId> key1==value1 key2=value2 key3:=23 -

# Make POST request with form data
$ registry-api.sh --host <hostname> <operationId> key1:=value1 key2:=value2 key3:=23

# Preview the cURL command without actually executing it
$ registry-api.sh --host http://<hostname>:<port> --dry-run <operationid>

```

## Docker image

You can easily create a Docker image containing a preconfigured environment
for using the REST Bash client including working autocompletion and short
welcome message with basic instructions, using the generated Dockerfile:

```shell
docker build -t my-rest-client .
docker run -it my-rest-client
```

By default you will be logged into a Zsh environment which has much more
advanced auto completion, but you can switch to Bash, where basic autocompletion
is also available.

## Shell completion

### Bash

The generated bash-completion script can be either directly loaded to the current Bash session using:

```shell
source registry-api.sh.bash-completion
```

Alternatively, the script can be copied to the `/etc/bash-completion.d` (or on OSX with Homebrew to `/usr/local/etc/bash-completion.d`):

```shell
sudo cp registry-api.sh.bash-completion /etc/bash-completion.d/registry-api.sh
```

#### OS X

On OSX you might need to install bash-completion using Homebrew:

```shell
brew install bash-completion
```

and add the following to the `~/.bashrc`:

```shell
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

### Zsh

In Zsh, the generated `_registry-api.sh` Zsh completion file must be copied to one of the folders under `$FPATH` variable.

## Documentation for API Endpoints

All URIs are relative to **

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*AccessCheckApi* | [**checkAdminAccess**](docs/AccessCheckApi.md#checkadminaccess) | **GET** /check-access/check-admin-access | Check Admin Access
*AccessCheckApi* | [**checkGeneralAccess**](docs/AccessCheckApi.md#checkgeneralaccess) | **GET** /check-access/check-general-access | Check General Access
*AccessCheckApi* | [**checkReadAccess**](docs/AccessCheckApi.md#checkreadaccess) | **GET** /check-access/check-read-access | Check Read Access
*AccessCheckApi* | [**checkWriteAccess**](docs/AccessCheckApi.md#checkwriteaccess) | **GET** /check-access/check-write-access | Check Write Access
*AdminApi* | [**registryAdminExport**](docs/AdminApi.md#registryadminexport) | **GET** /admin/export | Export Items
*AdminApi* | [**registryAdminImport**](docs/AdminApi.md#registryadminimport) | **POST** /admin/import | Import Items Parsed
*AdminApi* | [**registryAdminRestore**](docs/AdminApi.md#registryadminrestore) | **POST** /admin/restore_from_table | Restore From Table Parsed
*DatasetTemplateApi* | [**createEntityDatasetTemplate**](docs/DatasetTemplateApi.md#createentitydatasettemplate) | **POST** /registry/entity/dataset_template/create | Create Item
*DatasetTemplateApi* | [**deleteEntityDatasetTemplate**](docs/DatasetTemplateApi.md#deleteentitydatasettemplate) | **DELETE** /registry/entity/dataset_template/delete | Delete Item
*DatasetTemplateApi* | [**fetchEntityDatasetTemplate**](docs/DatasetTemplateApi.md#fetchentitydatasettemplate) | **GET** /registry/entity/dataset_template/fetch | Fetch Item
*DatasetTemplateApi* | [**listEntityDatasetTemplate**](docs/DatasetTemplateApi.md#listentitydatasettemplate) | **GET** /registry/entity/dataset_template/list | List Items
*DatasetTemplateApi* | [**schemaEntityDatasetTemplate**](docs/DatasetTemplateApi.md#schemaentitydatasettemplate) | **GET** /registry/entity/dataset_template/schema | Get Schema
*DatasetTemplateApi* | [**seedEntityDatasetTemplate**](docs/DatasetTemplateApi.md#seedentitydatasettemplate) | **POST** /registry/entity/dataset_template/seed | Seed Item
*DatasetTemplateApi* | [**uiSchemaEntityDatasetTemplate**](docs/DatasetTemplateApi.md#uischemaentitydatasettemplate) | **GET** /registry/entity/dataset_template/ui_schema | Get Ui Schema
*DatasetTemplateApi* | [**updateEntityDatasetTemplate**](docs/DatasetTemplateApi.md#updateentitydatasettemplate) | **PUT** /registry/entity/dataset_template/update | Update Item
*DatasetTemplateApi* | [**validateEntityDatasetTemplate**](docs/DatasetTemplateApi.md#validateentitydatasettemplate) | **POST** /registry/entity/dataset_template/validate | Validate
*DefaultApi* | [**root**](docs/DefaultApi.md#root) | **GET** / | Root
*GeneralRegistryApi* | [**fetch**](docs/GeneralRegistryApi.md#fetch) | **GET** /registry/general/fetch | Fetch Item
*GeneralRegistryApi* | [**list**](docs/GeneralRegistryApi.md#list) | **POST** /registry/general/list | List Items
*ModelApi* | [**createEntityModel**](docs/ModelApi.md#createentitymodel) | **POST** /registry/entity/model/create | Create Item
*ModelApi* | [**deleteEntityModel**](docs/ModelApi.md#deleteentitymodel) | **DELETE** /registry/entity/model/delete | Delete Item
*ModelApi* | [**fetchEntityModel**](docs/ModelApi.md#fetchentitymodel) | **GET** /registry/entity/model/fetch | Fetch Item
*ModelApi* | [**listEntityModel**](docs/ModelApi.md#listentitymodel) | **GET** /registry/entity/model/list | List Items
*ModelApi* | [**schemaEntityModel**](docs/ModelApi.md#schemaentitymodel) | **GET** /registry/entity/model/schema | Get Schema
*ModelApi* | [**seedEntityModel**](docs/ModelApi.md#seedentitymodel) | **POST** /registry/entity/model/seed | Seed Item
*ModelApi* | [**uiSchemaEntityModel**](docs/ModelApi.md#uischemaentitymodel) | **GET** /registry/entity/model/ui_schema | Get Ui Schema
*ModelApi* | [**updateEntityModel**](docs/ModelApi.md#updateentitymodel) | **PUT** /registry/entity/model/update | Update Item
*ModelApi* | [**validateEntityModel**](docs/ModelApi.md#validateentitymodel) | **POST** /registry/entity/model/validate | Validate
*ModelRunApi* | [**createActivityModelRun**](docs/ModelRunApi.md#createactivitymodelrun) | **POST** /registry/activity/model_run/create | Create Item
*ModelRunApi* | [**deleteActivityModelRun**](docs/ModelRunApi.md#deleteactivitymodelrun) | **DELETE** /registry/activity/model_run/delete | Delete Item
*ModelRunApi* | [**fetchActivityModelRun**](docs/ModelRunApi.md#fetchactivitymodelrun) | **GET** /registry/activity/model_run/fetch | Fetch Item
*ModelRunApi* | [**listActivityModelRun**](docs/ModelRunApi.md#listactivitymodelrun) | **GET** /registry/activity/model_run/list | List Items
*ModelRunApi* | [**schemaActivityModelRun**](docs/ModelRunApi.md#schemaactivitymodelrun) | **GET** /registry/activity/model_run/schema | Get Schema
*ModelRunApi* | [**seedActivityModelRun**](docs/ModelRunApi.md#seedactivitymodelrun) | **POST** /registry/activity/model_run/seed | Seed Item
*ModelRunApi* | [**uiSchemaActivityModelRun**](docs/ModelRunApi.md#uischemaactivitymodelrun) | **GET** /registry/activity/model_run/ui_schema | Get Ui Schema
*ModelRunApi* | [**updateActivityModelRun**](docs/ModelRunApi.md#updateactivitymodelrun) | **PUT** /registry/activity/model_run/update | Update Item
*ModelRunApi* | [**validateActivityModelRun**](docs/ModelRunApi.md#validateactivitymodelrun) | **POST** /registry/activity/model_run/validate | Validate
*ModelRunWorkflowDefinitionApi* | [**createEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#createentitymodelrunworkflowdefinition) | **POST** /registry/entity/model_run_workflow/create | Create Item
*ModelRunWorkflowDefinitionApi* | [**deleteEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#deleteentitymodelrunworkflowdefinition) | **DELETE** /registry/entity/model_run_workflow/delete | Delete Item
*ModelRunWorkflowDefinitionApi* | [**fetchEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#fetchentitymodelrunworkflowdefinition) | **GET** /registry/entity/model_run_workflow/fetch | Fetch Item
*ModelRunWorkflowDefinitionApi* | [**listEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#listentitymodelrunworkflowdefinition) | **GET** /registry/entity/model_run_workflow/list | List Items
*ModelRunWorkflowDefinitionApi* | [**schemaEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#schemaentitymodelrunworkflowdefinition) | **GET** /registry/entity/model_run_workflow/schema | Get Schema
*ModelRunWorkflowDefinitionApi* | [**seedEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#seedentitymodelrunworkflowdefinition) | **POST** /registry/entity/model_run_workflow/seed | Seed Item
*ModelRunWorkflowDefinitionApi* | [**uiSchemaEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#uischemaentitymodelrunworkflowdefinition) | **GET** /registry/entity/model_run_workflow/ui_schema | Get Ui Schema
*ModelRunWorkflowDefinitionApi* | [**updateEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#updateentitymodelrunworkflowdefinition) | **PUT** /registry/entity/model_run_workflow/update | Update Item
*ModelRunWorkflowDefinitionApi* | [**validateEntityModelRunWorkflowDefinition**](docs/ModelRunWorkflowDefinitionApi.md#validateentitymodelrunworkflowdefinition) | **POST** /registry/entity/model_run_workflow/validate | Validate
*OrganisationApi* | [**createAgentOrganisation**](docs/OrganisationApi.md#createagentorganisation) | **POST** /registry/agent/organisation/create | Create Item
*OrganisationApi* | [**deleteAgentOrganisation**](docs/OrganisationApi.md#deleteagentorganisation) | **DELETE** /registry/agent/organisation/delete | Delete Item
*OrganisationApi* | [**fetchAgentOrganisation**](docs/OrganisationApi.md#fetchagentorganisation) | **GET** /registry/agent/organisation/fetch | Fetch Item
*OrganisationApi* | [**listAgentOrganisation**](docs/OrganisationApi.md#listagentorganisation) | **GET** /registry/agent/organisation/list | List Items
*OrganisationApi* | [**schemaAgentOrganisation**](docs/OrganisationApi.md#schemaagentorganisation) | **GET** /registry/agent/organisation/schema | Get Schema
*OrganisationApi* | [**seedAgentOrganisation**](docs/OrganisationApi.md#seedagentorganisation) | **POST** /registry/agent/organisation/seed | Seed Item
*OrganisationApi* | [**uiSchemaAgentOrganisation**](docs/OrganisationApi.md#uischemaagentorganisation) | **GET** /registry/agent/organisation/ui_schema | Get Ui Schema
*OrganisationApi* | [**updateAgentOrganisation**](docs/OrganisationApi.md#updateagentorganisation) | **PUT** /registry/agent/organisation/update | Update Item
*OrganisationApi* | [**validateAgentOrganisation**](docs/OrganisationApi.md#validateagentorganisation) | **POST** /registry/agent/organisation/validate | Validate
*PersonApi* | [**createAgentPerson**](docs/PersonApi.md#createagentperson) | **POST** /registry/agent/person/create | Create Item
*PersonApi* | [**deleteAgentPerson**](docs/PersonApi.md#deleteagentperson) | **DELETE** /registry/agent/person/delete | Delete Item
*PersonApi* | [**fetchAgentPerson**](docs/PersonApi.md#fetchagentperson) | **GET** /registry/agent/person/fetch | Fetch Item
*PersonApi* | [**listAgentPerson**](docs/PersonApi.md#listagentperson) | **GET** /registry/agent/person/list | List Items
*PersonApi* | [**schemaAgentPerson**](docs/PersonApi.md#schemaagentperson) | **GET** /registry/agent/person/schema | Get Schema
*PersonApi* | [**seedAgentPerson**](docs/PersonApi.md#seedagentperson) | **POST** /registry/agent/person/seed | Seed Item
*PersonApi* | [**uiSchemaAgentPerson**](docs/PersonApi.md#uischemaagentperson) | **GET** /registry/agent/person/ui_schema | Get Ui Schema
*PersonApi* | [**updateAgentPerson**](docs/PersonApi.md#updateagentperson) | **PUT** /registry/agent/person/update | Update Item
*PersonApi* | [**validateAgentPerson**](docs/PersonApi.md#validateagentperson) | **POST** /registry/agent/person/validate | Validate


## Documentation For Models

 - [AdditionalDescription](docs/AdditionalDescription.md)
 - [AssociationInfo](docs/AssociationInfo.md)
 - [AutomationSchedule](docs/AutomationSchedule.md)
 - [ColumnIndex](docs/ColumnIndex.md)
 - [ColumnName](docs/ColumnName.md)
 - [CompleteItemCount](docs/CompleteItemCount.md)
 - [CreatedItem](docs/CreatedItem.md)
 - [CreatedItem1](docs/CreatedItem1.md)
 - [CreatedItem2](docs/CreatedItem2.md)
 - [CreatedItem3](docs/CreatedItem3.md)
 - [CreatedItem4](docs/CreatedItem4.md)
 - [CreatedItem5](docs/CreatedItem5.md)
 - [Credentials](docs/Credentials.md)
 - [DataStoreDatasetResource](docs/DataStoreDatasetResource.md)
 - [Dataset](docs/Dataset.md)
 - [DatasetParameter](docs/DatasetParameter.md)
 - [DatasetStructuralTemplate](docs/DatasetStructuralTemplate.md)
 - [DatasetTemplateCreateResponse](docs/DatasetTemplateCreateResponse.md)
 - [DatasetTemplateDomainInfo](docs/DatasetTemplateDomainInfo.md)
 - [DatasetTemplateFetchResponse](docs/DatasetTemplateFetchResponse.md)
 - [DatasetTemplateListResponse](docs/DatasetTemplateListResponse.md)
 - [DatasetTemplateSeedResponse](docs/DatasetTemplateSeedResponse.md)
 - [DatasetTemporalInformation](docs/DatasetTemporalInformation.md)
 - [DatasetType](docs/DatasetType.md)
 - [DatasetUsageInformation](docs/DatasetUsageInformation.md)
 - [DatasetUsageType](docs/DatasetUsageType.md)
 - [Description](docs/Description.md)
 - [Email](docs/Email.md)
 - [EnforceConstraints](docs/EnforceConstraints.md)
 - [EnforceSizeConstraints](docs/EnforceSizeConstraints.md)
 - [Extension](docs/Extension.md)
 - [FailureList](docs/FailureList.md)
 - [FileInformation](docs/FileInformation.md)
 - [FileSystemResource](docs/FileSystemResource.md)
 - [FilenameRegex](docs/FilenameRegex.md)
 - [Folder](docs/Folder.md)
 - [HTTPValidationError](docs/HTTPValidationError.md)
 - [ImportMode](docs/ImportMode.md)
 - [ImportStatistics](docs/ImportStatistics.md)
 - [InputInfo](docs/InputInfo.md)
 - [Item](docs/Item.md)
 - [Item1](docs/Item1.md)
 - [Item2](docs/Item2.md)
 - [Item3](docs/Item3.md)
 - [Item4](docs/Item4.md)
 - [Item5](docs/Item5.md)
 - [Item6](docs/Item6.md)
 - [ItemCategory](docs/ItemCategory.md)
 - [ItemDatasetTemplate](docs/ItemDatasetTemplate.md)
 - [ItemIsSeed](docs/ItemIsSeed.md)
 - [ItemModel](docs/ItemModel.md)
 - [ItemModelRun](docs/ItemModelRun.md)
 - [ItemModelRunWorkflowDefinition](docs/ItemModelRunWorkflowDefinition.md)
 - [ItemOrganisation](docs/ItemOrganisation.md)
 - [ItemPerson](docs/ItemPerson.md)
 - [ItemSubType](docs/ItemSubType.md)
 - [Items](docs/Items.md)
 - [Items1](docs/Items1.md)
 - [Items2](docs/Items2.md)
 - [Items3](docs/Items3.md)
 - [Items4](docs/Items4.md)
 - [Items5](docs/Items5.md)
 - [Items6](docs/Items6.md)
 - [Items7](docs/Items7.md)
 - [JsonSchema](docs/JsonSchema.md)
 - [JsonSchemaResponse](docs/JsonSchemaResponse.md)
 - [LocationInner](docs/LocationInner.md)
 - [ModelCreateResponse](docs/ModelCreateResponse.md)
 - [ModelDomainInfo](docs/ModelDomainInfo.md)
 - [ModelFetchResponse](docs/ModelFetchResponse.md)
 - [ModelListResponse](docs/ModelListResponse.md)
 - [ModelRunCreateResponse](docs/ModelRunCreateResponse.md)
 - [ModelRunDomainInfo](docs/ModelRunDomainInfo.md)
 - [ModelRunFetchResponse](docs/ModelRunFetchResponse.md)
 - [ModelRunListResponse](docs/ModelRunListResponse.md)
 - [ModelRunRecord](docs/ModelRunRecord.md)
 - [ModelRunSeedResponse](docs/ModelRunSeedResponse.md)
 - [ModelRunWorkflowDefinitionCreateResponse](docs/ModelRunWorkflowDefinitionCreateResponse.md)
 - [ModelRunWorkflowDefinitionDomainInfo](docs/ModelRunWorkflowDefinitionDomainInfo.md)
 - [ModelRunWorkflowDefinitionFetchResponse](docs/ModelRunWorkflowDefinitionFetchResponse.md)
 - [ModelRunWorkflowDefinitionListResponse](docs/ModelRunWorkflowDefinitionListResponse.md)
 - [ModelRunWorkflowDefinitionResource](docs/ModelRunWorkflowDefinitionResource.md)
 - [ModelRunWorkflowDefinitionSeedResponse](docs/ModelRunWorkflowDefinitionSeedResponse.md)
 - [ModelSeedResponse](docs/ModelSeedResponse.md)
 - [ModellerResource](docs/ModellerResource.md)
 - [Orcid](docs/Orcid.md)
 - [OrganisationCreateResponse](docs/OrganisationCreateResponse.md)
 - [OrganisationDomainInfo](docs/OrganisationDomainInfo.md)
 - [OrganisationFetchResponse](docs/OrganisationFetchResponse.md)
 - [OrganisationListResponse](docs/OrganisationListResponse.md)
 - [OrganisationResource](docs/OrganisationResource.md)
 - [OrganisationSeedResponse](docs/OrganisationSeedResponse.md)
 - [OutputInfo](docs/OutputInfo.md)
 - [ParameterName](docs/ParameterName.md)
 - [Parameters](docs/Parameters.md)
 - [Path](docs/Path.md)
 - [PersonCreateResponse](docs/PersonCreateResponse.md)
 - [PersonDomainInfo](docs/PersonDomainInfo.md)
 - [PersonFetchResponse](docs/PersonFetchResponse.md)
 - [PersonListResponse](docs/PersonListResponse.md)
 - [PersonSeedResponse](docs/PersonSeedResponse.md)
 - [QueryFilter](docs/QueryFilter.md)
 - [QueryFilterItemCategory](docs/QueryFilterItemCategory.md)
 - [QueryFilterItemSubtype](docs/QueryFilterItemSubtype.md)
 - [QueryRecordTypes](docs/QueryRecordTypes.md)
 - [RecordType](docs/RecordType.md)
 - [RegistryExportResponse](docs/RegistryExportResponse.md)
 - [RegistryImportRequest](docs/RegistryImportRequest.md)
 - [RegistryImportResponse](docs/RegistryImportResponse.md)
 - [RegistryRestoreRequest](docs/RegistryRestoreRequest.md)
 - [RequestingOrganisation](docs/RequestingOrganisation.md)
 - [Ror](docs/Ror.md)
 - [SeedItemCount](docs/SeedItemCount.md)
 - [SeedItems](docs/SeedItems.md)
 - [SeededItem](docs/SeededItem.md)
 - [SizeEstimate](docs/SizeEstimate.md)
 - [SizeMax](docs/SizeMax.md)
 - [SizeMin](docs/SizeMin.md)
 - [SpatialInformation](docs/SpatialInformation.md)
 - [Statistics](docs/Statistics.md)
 - [Status](docs/Status.md)
 - [StatusResponse](docs/StatusResponse.md)
 - [StructuralTemplate](docs/StructuralTemplate.md)
 - [TemplateResource](docs/TemplateResource.md)
 - [TemplatedDataset](docs/TemplatedDataset.md)
 - [TemporalInformation](docs/TemporalInformation.md)
 - [TotalItemCount](docs/TotalItemCount.md)
 - [URLDatasetResource](docs/URLDatasetResource.md)
 - [UiSchema](docs/UiSchema.md)
 - [UiSchemaResponse](docs/UiSchemaResponse.md)
 - [UnparsableItemCount](docs/UnparsableItemCount.md)
 - [UnparsableItems](docs/UnparsableItems.md)
 - [UnparsedListResponse](docs/UnparsedListResponse.md)
 - [UntypedFetchResponse](docs/UntypedFetchResponse.md)
 - [Usage](docs/Usage.md)
 - [User](docs/User.md)
 - [ValidationError](docs/ValidationError.md)
 - [Version](docs/Version.md)
 - [VocabularyId](docs/VocabularyId.md)
 - [WorkflowRunCompletionStatus](docs/WorkflowRunCompletionStatus.md)


## Documentation For Authorization


## OAuth2PasswordBearer


- **Type**: OAuth
- **Flow**: password
- **Token URL**: token
- **Scopes**: N/A

