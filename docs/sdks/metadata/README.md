# Metadata

## Overview

### Available Operations

* [List](#list) - List metadata
* [GetPredefinedConfigs](#getpredefinedconfigs) - List predefined configs

## List

Retrieve available shipment metadata, including carriers, services, paper types, envelopes and other configuration options.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## GetPredefinedConfigs

Retrieve the predefined shipment configuration profiles stored in your account, including their configuration options.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |