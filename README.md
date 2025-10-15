[![NuGet Version](https://img.shields.io/nuget/v/Postivo)](https://www.nuget.org/packages/Postivo)
[![GitHub License](https://img.shields.io/github/license/postivo/csharp-client)](https://github.com/postivo/csharp-client/blob/main/LICENSE)
[![Static Badge](https://img.shields.io/badge/built_by-Speakeasy-yellow)](https://www.speakeasy.com/?utm_source=postivo&utm_campaign=csharp)

# POSTIVO.PL REST API Client SDK for C#

This package provides the **POSTIVO.PL Hybrid Mail Services SDK** for C#, allowing you to dispatch shipments directly from your application via the [POSTIVO.PL](https://postivo.pl) platform.

## Additional documentation:

Comprehensive documentation of all methods and types is available below in [Available Resources and Operations](#available-resources-and-operations).

You can also refer to the [REST API v1 documentation](https://api.postivo.pl/rest/v1/) for additional details about this SDK.

<!-- No Summary [summary] -->
<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [POSTIVO.PL REST API Client SDK for C](#postivopl-rest-api-client-sdk-for-c)
  * [Additional documentation:](#additional-documentation)
  * [SDK Installation](#sdk-installation)
  * [Requirements:](#requirements)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

### NuGet

To add the [NuGet](https://www.nuget.org/) package to a .NET project:
```bash
dotnet add package Postivo
```

### Locally

To add a reference to a local instance of the SDK in a .NET project:
```bash
dotnet add reference src/Postivo/Postivo.csproj
```
<!-- End SDK Installation [installation] -->
## Requirements:
- Minimal .NET Runtime version: 8.0
<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Sending Shipment to single recipient

This example demonstrates simple sending Shipment to a single recipient:

```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Shipment req = new Shipment() {
    Recipients = ShipmentRecipients.CreateRecipients(
        Recipients.CreateRecipientInline(
            new RecipientInline() {
                Name = "Jan Nowak",
                Name2 = "Firma testowa Sp. z o.o.",
                Address = "ul. Testowa",
                HomeNumber = "23",
                FlatNumber = "2",
                PostCode = "00-999",
                City = "Warszawa",
                PhoneNumber = "+48666666666",
                Postscript = "Komunikat",
                CustomId = "1234567890",
            }
        )
    ),
    Documents = ShipmentDocuments.CreateArrayOfDocuments(
        new List<Documents>() {
            Documents.CreateDocumentPdf(
                new DocumentPdf() {
                    FileStream = "<document_1 content encoded to base64>",
                    FileName = "document1.pdf",
                }
            ),
            Documents.CreateDocumentPdf(
                new DocumentPdf() {
                    FileStream = "<document_2 content encoded to base64>",
                    FileName = "document2.pdf",
                }
            ),
        }
    ),
    Options = Options.CreateRequestOptions(
        new RequestOptions() {
            PredefinedConfigId = 2670,
        }
    ),
};

var res = await sdk.Shipments.DispatchAsync(req);

// handle response
```

### Checking the price of a shipment for single recipient

This example demonstrates simple checking the price of a Shipment to a single recipient:

```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Shipment req = new Shipment() {
    Recipients = ShipmentRecipients.CreateRecipients(
        Recipients.CreateRecipientInline(
            new RecipientInline() {
                Name = "Jan Nowak",
                Name2 = "Firma testowa Sp. z o.o.",
                Address = "ul. Testowa",
                HomeNumber = "23",
                FlatNumber = "2",
                PostCode = "00-999",
                City = "Warszawa",
                PhoneNumber = "+48666666666",
                Postscript = "Komunikat",
                CustomId = "1234567890",
            }
        )
    ),
    Documents = ShipmentDocuments.CreateArrayOfDocuments(
        new List<Documents>() {
            Documents.CreateDocumentPdf(
                new DocumentPdf() {
                    FileStream = "<document_1 content encoded to base64>",
                    FileName = "document1.pdf",
                }
            ),
            Documents.CreateDocumentPdf(
                new DocumentPdf() {
                    FileStream = "<document_2 content encoded to base64>",
                    FileName = "document2.pdf",
                }
            ),
        }
    ),
    Options = Options.CreateRequestOptions(
        new RequestOptions() {
            PredefinedConfigId = 2670,
        }
    ),
};

var res = await sdk.Shipments.PriceAsync(req);

// handle response
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name     | Type | Scheme      |
| -------- | ---- | ----------- |
| `Bearer` | http | HTTP Bearer |

To authenticate with the API the `Bearer` parameter must be set when initializing the SDK client instance. For example:
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Accounts.GetAsync();

// handle response
```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Accounts](docs/sdks/accounts/README.md)

* [Get](docs/sdks/accounts/README.md#get) - Retrieve account details
* [GetSubaccount](docs/sdks/accounts/README.md#getsubaccount) - Get subaccount details

#### [AddressBook.Contacts](docs/sdks/contacts/README.md)

* [List](docs/sdks/contacts/README.md#list) - List contacts
* [Add](docs/sdks/contacts/README.md#add) - Add a new contact
* [Get](docs/sdks/contacts/README.md#get) - Retrieve contact details
* [Update](docs/sdks/contacts/README.md#update) - Update a contact
* [Delete](docs/sdks/contacts/README.md#delete) - Delete a contact
* [RemoveFromGroup](docs/sdks/contacts/README.md#removefromgroup) - Remove a contact from a group
* [AddToGroup](docs/sdks/contacts/README.md#addtogroup) - Add a contact to a group

#### [AddressBook.Contacts.ByExtId](docs/sdks/byextid/README.md)

* [Get](docs/sdks/byextid/README.md#get) - Retrieve contact details by EXT_ID
* [Update](docs/sdks/byextid/README.md#update) - Update a contact by EXT_ID
* [Delete](docs/sdks/byextid/README.md#delete) - Delete a contact by EXT_ID
* [RemoveFromGroup](docs/sdks/byextid/README.md#removefromgroup) - Remove a contact from a group by EXT_ID
* [AddToGroup](docs/sdks/byextid/README.md#addtogroup) - Add a contact to a group by EXT_ID

#### [AddressBook.Groups](docs/sdks/groups/README.md)

* [List](docs/sdks/groups/README.md#list) - List groups
* [Add](docs/sdks/groups/README.md#add) - Add a new group
* [Get](docs/sdks/groups/README.md#get) - Retrieve group details
* [Update](docs/sdks/groups/README.md#update) - Update a group
* [Delete](docs/sdks/groups/README.md#delete) - Delete a group

### [Common](docs/sdks/common/README.md)

* [Ping](docs/sdks/common/README.md#ping) - Check API availability and version

### [Metadata](docs/sdks/metadata/README.md)

* [List](docs/sdks/metadata/README.md#list) - List metadata
* [GetPredefinedConfigs](docs/sdks/metadata/README.md#getpredefinedconfigs) - List predefined configs

### [Senders](docs/sdks/senders/README.md)

* [List](docs/sdks/senders/README.md#list) - List senders
* [Add](docs/sdks/senders/README.md#add) - Add a new sender
* [Delete](docs/sdks/senders/README.md#delete) - Delete a sender
* [Verify](docs/sdks/senders/README.md#verify) - Verify sender

### [Shipments](docs/sdks/shipments/README.md)

* [Status](docs/sdks/shipments/README.md#status) - Retrieve shipment details with status events
* [Cancel](docs/sdks/shipments/README.md#cancel) - Cancel shipments
* [Dispatch](docs/sdks/shipments/README.md#dispatch) - Dispatch a new shipment
* [Documents](docs/sdks/shipments/README.md#documents) - Retrieve documents related to a shipment
* [Price](docs/sdks/shipments/README.md#price) - Check the shipment price

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply pass a `RetryConfig` to the call:
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Accounts.GetAsync(retryConfig: new RetryConfig(
    strategy: RetryConfig.RetryStrategy.BACKOFF,
    backoff: new BackoffStrategy(
        initialIntervalMs: 1L,
        maxIntervalMs: 50L,
        maxElapsedTimeMs: 100L,
        exponent: 1.1
    ),
    retryConnectionErrors: false
));

// handle response
```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `RetryConfig` optional parameter when intitializing the SDK:
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(
    retryConfig: new RetryConfig(
        strategy: RetryConfig.RetryStrategy.BACKOFF,
        backoff: new BackoffStrategy(
            initialIntervalMs: 1L,
            maxIntervalMs: 50L,
            maxElapsedTimeMs: 100L,
            exponent: 1.1
        ),
        retryConnectionErrors: false
    ),
    bearer: "<YOUR API ACCESS TOKEN>"
);

var res = await sdk.Accounts.GetAsync();

// handle response
```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`ClientException`](./src/Postivo/Models/Errors/ClientException.cs) is the base exception class for all HTTP error responses. It has the following properties:

| Property      | Type                  | Description           |
|---------------|-----------------------|-----------------------|
| `Message`     | *string*              | Error message         |
| `Request`     | *HttpRequestMessage*  | HTTP request object   |
| `Response`    | *HttpResponseMessage* | HTTP response object  |

Some exceptions in this SDK include an additional `Payload` field, which will contain deserialized custom error data when present. Possible exceptions are listed in the [Error Classes](#error-classes) section.

### Example

```csharp
using Postivo;
using Postivo.Models.Components;
using Postivo.Models.Errors;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

try
{
    var res = await sdk.Accounts.GetAsync();

    // handle response
}
catch (ClientException ex)  // all SDK exceptions inherit from ClientException
{
    // ex.ToString() provides a detailed error message
    System.Console.WriteLine(ex);

    // Base exception fields
    HttpRequestMessage request = ex.Request;
    HttpResponseMessage response = ex.Response;
    var statusCode = (int)response.StatusCode;
    var responseBody = ex.Body;

    if (ex is Models.Errors.ErrorResponse) // different exceptions may be thrown depending on the method
    {
        // Check error data fields
        Models.Errors.ErrorResponsePayload payload = ex.Payload;
        string Type = payload.Type;
        long Status = payload.Status;
        // ...
    }

    // An underlying cause may be provided
    if (ex.InnerException != null)
    {
        Exception cause = ex.InnerException;
    }
}
catch (OperationCanceledException ex)
{
    // CancellationToken was cancelled
}
catch (System.Net.Http.HttpRequestException ex)
{
    // Check ex.InnerException for Network connectivity errors
}
```

### Error Classes

**Primary exceptions:**
* [`ClientException`](./src/Postivo/Models/Errors/ClientException.cs): The base class for HTTP error responses.
  * [`ErrorResponse`](./src/Postivo/Models/Errors/ErrorResponse.cs): Problem Details object (RFC 9457) describing the error.

<details><summary>Less common exceptions (2)</summary>

* [`System.Net.Http.HttpRequestException`](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httprequestexception): Network connectivity error. For more details about the underlying cause, inspect the `ex.InnerException`.

* Inheriting from [`ClientException`](./src/Postivo/Models/Errors/ClientException.cs):
  * [`ResponseValidationError`](./src/Postivo/Models/Errors/ResponseValidationError.cs): Thrown when the response data could not be deserialized into the expected type.
</details>
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally by passing a server name to the `server: string` optional parameter when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name      | Server                                   | Description           |
| --------- | ---------------------------------------- | --------------------- |
| `prod`    | `https://api.postivo.pl/rest/v1`         | Production system     |
| `sandbox` | `https://api.postivo.pl/rest-sandbox/v1` | Test system (SANDBOX) |

#### Example

```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(
    server: SDKConfig.Server.Sandbox,
    bearer: "<YOUR API ACCESS TOKEN>"
);

var res = await sdk.Accounts.GetAsync();

// handle response
```

### Override Server URL Per-Client

The default server can also be overridden globally by passing a URL to the `serverUrl: string` optional parameter when initializing the SDK client instance. For example:
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(
    serverUrl: "https://api.postivo.pl/rest/v1",
    bearer: "<YOUR API ACCESS TOKEN>"
);

var res = await sdk.Accounts.GetAsync();

// handle response
```
<!-- End Server Selection [server] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release.