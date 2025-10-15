# Common
(*Common*)

## Overview

Common

### Available Operations

* [Ping](#ping) - Check API availability and version

## Ping

Check the API connection and current availability status. The response also includes the current API version.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="ping" method="get" path="/ping" -->
```csharp
using Postivo;

var sdk = new Client();

var res = await sdk.Common.PingAsync();

// handle response
```

### Response

**[Models.Requests.PingResponse](../../Models/Requests/PingResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 4XX                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 503, 5XX                            | application/problem+json            |