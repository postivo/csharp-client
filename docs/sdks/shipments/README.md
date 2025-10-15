# Shipments
(*Shipments*)

## Overview

### Available Operations

* [Status](#status) - Retrieve shipment details with status events
* [Cancel](#cancel) - Cancel shipments
* [Dispatch](#dispatch) - Dispatch a new shipment
* [Documents](#documents) - Retrieve documents related to a shipment
* [Price](#price) - Check the shipment price

## Status

Retrieve the current status and details for one or more shipments by their `ids`. Pass the unique shipment IDs (returned when the shipments were created) as a path parameter. To query provide a list (up to **50** IDs per call). For larger batches, split the requests.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getStatus" method="get" path="/shipment/{ids}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Shipments.StatusAsync(ids: new List<string>() {
    "A0043456",
});

// handle response
```

### Parameters

| Parameter                                                                                                           | Type                                                                                                                | Required                                                                                                            | Description                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `Ids`                                                                                                               | List<*string*>                                                                                                      | :heavy_check_mark:                                                                                                  | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. |

### Response

**[GetStatusResponse](../../Models/Requests/GetStatusResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Cancel

Cancel shipments that have not yet been processed by their `ids`. Pass the unique shipment IDs (returned when the shipment was created) as a parameter. To cancel multiple shipments at once, provide a list of IDs (up to **50** per call). For larger volumes, split the operation into multiple requests. Only shipments with status `ACCEPTED` can be cancelled.

If duplicate shipment IDs are provided in a single call, the API processes each unique ID only once.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="cancelShipment" method="delete" path="/shipment/{ids}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Shipments.CancelAsync(ids: new List<string>() {
    "A0043456",
});

// handle response
```

### Parameters

| Parameter                                                                                                           | Type                                                                                                                | Required                                                                                                            | Description                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `Ids`                                                                                                               | List<*string*>                                                                                                      | :heavy_check_mark:                                                                                                  | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. |

### Response

**[CancelShipmentResponse](../../Models/Requests/CancelShipmentResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Dispatch

Send a shipment to one or multiple recipients in a single request. Provide a `Shipment` object. The object includes properties that define the shipment (recipient details, included documents, and optional settings). Some fields are required.

The system accepts up to **50** recipients per call. For larger volumes, split the operation into multiple requests.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="shipmentDispatch" method="post" path="/shipment" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Shipment req = new Shipment() {
    Recipients = Recipients2.CreateRecipientInline(
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
    ),
    Documents = Documents2.CreateArrayOfDocuments1(
        new List<Documents1>() {
            Documents1.CreateDocumentPdf(
                new DocumentPdf() {
                    FileStream = "<document_1 content encoded to base64>",
                    FileName = "document1.pdf",
                }
            ),
            Documents1.CreateDocumentPdf(
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

### Parameters

| Parameter                                       | Type                                            | Required                                        | Description                                     |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `request`                                       | [Shipment](../../Models/Components/Shipment.md) | :heavy_check_mark:                              | The request object to use for the request.      |

### Response

**[ShipmentDispatchResponse](../../Models/Requests/ShipmentDispatchResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Documents

Download documents related to a shipment by its `id`. Pass the unique shipment `id` (returned when the shipment was created) as a parameter. The second parameter is the document type to download. Supported document types include: dispatch certificate, envelope template, and EPO (in PDF or XML formats).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getDocuments" method="get" path="/shipment/{id}/document/{type}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using Postivo.Models.Requests;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Shipments.DocumentsAsync(
    id: "A0043456",
    type: DocumentType.DispatchCert
);

// handle response
```

### Parameters

| Parameter                                                                | Type                                                                     | Required                                                                 | Description                                                              | Example                                                                  |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `Id`                                                                     | *string*                                                                 | :heavy_check_mark:                                                       | Single shipment ID assigned by the system when the shipment was created. | A0043456                                                                 |
| `Type`                                                                   | [DocumentType](../../Models/Requests/DocumentType.md)                    | :heavy_check_mark:                                                       | Type of document/certificate to generate.                                | dispatch_cert                                                            |

### Response

**[GetDocumentsResponse](../../Models/Requests/GetDocumentsResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Price

Check the price of a shipment for one or multiple recipients. Provide a `Shipment` object in the request. Each object includes properties such as recipient details, included documents, and optional settings. Some fields are required.

The system accepts up to **50** recipients per call. For larger volumes, split the operation into multiple requests.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="shipmentPrice" method="post" path="/shipment/price" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Shipment req = new Shipment() {
    Recipients = Recipients2.CreateRecipientInline(
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
    ),
    Documents = Documents2.CreateArrayOfDocuments1(
        new List<Documents1>() {
            Documents1.CreateDocumentPdf(
                new DocumentPdf() {
                    FileStream = "<document_1 content encoded to base64>",
                    FileName = "document1.pdf",
                }
            ),
            Documents1.CreateDocumentPdf(
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

### Parameters

| Parameter                                       | Type                                            | Required                                        | Description                                     |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `request`                                       | [Shipment](../../Models/Components/Shipment.md) | :heavy_check_mark:                              | The request object to use for the request.      |

### Response

**[ShipmentPriceResponse](../../Models/Requests/ShipmentPriceResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |