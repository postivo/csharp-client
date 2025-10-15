# Metadata
(*Metadata*)

## Overview

### Available Operations

* [List](#list) - List metadata
* [GetPredefinedConfigs](#getpredefinedconfigs) - List predefined configs

## List

Retrieve a complete list of all types for shipments and their possible values. The method has no body and takes no parameters. The response includes metadata such as carrier types, service types, and more.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listMetadata" method="get" path="/metadata" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Metadata.ListAsync();

// handle response
```

### Response

**[ListMetadataResponse](../../Models/Requests/ListMetadataResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## GetPredefinedConfigs

Retrieve a complete list of predefined shipment configurations. The method has no body and takes no parameters. The response includes all stored configuration options.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listPredefinedConfigs" method="get" path="/metadata/predefined-configs" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Metadata.GetPredefinedConfigsAsync();

// handle response
```

### Response

**[ListPredefinedConfigsResponse](../../Models/Requests/ListPredefinedConfigsResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |