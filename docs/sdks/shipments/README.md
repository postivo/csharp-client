# Shipments

## Overview

### Available Operations

* [Status](#status) - Retrieve shipment details with status events
* [Cancel](#cancel) - Cancel shipments
* [Dispatch](#dispatch) - Dispatch a new shipment
* [Documents](#documents) - Retrieve documents related to a shipment
* [Price](#price) - Check the shipment price

## Status

Retrieve the current status and details for up to **50 shipments** using the IDs assigned when they were created. Separate multiple IDs with commas. Duplicate IDs are processed once.

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

| Parameter                                                                                                                                                                                                                                                                            | Type                                                                                                                                                                                                                                                                                 | Required                                                                                                                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Ids`                                                                                                                                                                                                                                                                                | List<*string*>                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                   | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. Empty items, including leading, trailing or repeated commas, are rejected with HTTP 400. Surrounding whitespace is ignored and duplicate IDs are processed once. |

### Response

**[GetStatusResponse](../../Models/Requests/GetStatusResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Cancel

Cancel up to **50 shipments** using the IDs assigned when they were created. Separate multiple IDs with commas. Only shipments with status `ACCEPTED` can be cancelled; duplicate IDs are processed once.

Check the result for each shipment, as individual cancellations can succeed or fail independently. If processing is interrupted, earlier cancellations may already have completed; check shipment status before retrying.

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

| Parameter                                                                                                                                                                                                                                                                            | Type                                                                                                                                                                                                                                                                                 | Required                                                                                                                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Ids`                                                                                                                                                                                                                                                                                | List<*string*>                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                   | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. Empty items, including leading, trailing or repeated commas, are rejected with HTTP 400. Surrounding whitespace is ignored and duplicate IDs are processed once. |

### Response

**[CancelShipmentResponse](../../Models/Requests/CancelShipmentResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Dispatch

Submit shipments for up to **50 recipients** using their addresses or Address Book identifiers, documents and optional shipment settings. For larger batches, split the operation into multiple calls. Check each recipient result, as individual shipments can succeed or fail independently.

### Example Usage: advanced_config

<!-- UsageSnippet language="csharp" operationID="shipmentDispatch" method="post" path="/shipment" example="advanced_config" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System;

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
    Documents = ShipmentDocuments.CreateDocuments(
        Documents.CreateDocumentPdf(
            new DocumentPdf() {
                FileStream = "<document content encoded to base64>",
                FileName = "document.pdf",
            }
        )
    ),
    Options = Options.CreateShipmentOptions(
        new ShipmentOptions() {
            PredefinedConfigId = 2670,
            InlineConfig = InlineConfigUnion.CreateInlineConfig(
                new InlineConfig() {
                    CarrierId = 4,
                    ServiceId = 16,
                    PaperId = 1,
                    ColorPrint = true,
                    DuplexPrint = false,
                    EnvelopeId = 454,
                    EnvelopeColorPrint = true,
                }
            ),
            SenderId = 1,
            DispatchDate = DateOnly.Parse("2025-10-21"),
            Callback = CallbackUnion.CreateCallback(
                new Callback() {
                    Url = "https://example.com/test",
                    UserToken = "75gh28hugjy8gfv6...",
                }
            ),
            MiscInfo = MiscInfoUnion.CreateMiscInfo(
                new MiscInfo() {
                    Mpk = "dział sprzedaży",
                    OrderName = "Wysyłka zaproszeń do Klientów",
                }
            ),
            RotateDocuments = true,
        }
    ),
};

var res = await sdk.Shipments.DispatchAsync(req);

// handle response
```
### Example Usage: multi

<!-- UsageSnippet language="csharp" operationID="shipmentDispatch" method="post" path="/shipment" example="multi" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Shipment req = new Shipment() {
    Recipients = ShipmentRecipients.CreateArrayOfRecipients(
        new List<Recipients>() {
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
            ),
            Recipients.CreateRecipientInline(
                new RecipientInline() {
                    Name = "Andrzej Kowalski",
                    Address = "ul. Przykładowa 45/321",
                    PostCode = "34-001",
                    City = "Kraków",
                    PhoneNumber = "+48999888777",
                    CustomId = "my-id-1113",
                }
            ),
        }
    ),
    Documents = ShipmentDocuments.CreateDocuments(
        Documents.CreateDocumentPdf(
            new DocumentPdf() {
                FileStream = "<document content encoded to base64>",
                FileName = "document.pdf",
            }
        )
    ),
    Options = Options.CreateShipmentOptions(
        new ShipmentOptions() {
            PredefinedConfigId = 2670,
        }
    ),
};

var res = await sdk.Shipments.DispatchAsync(req);

// handle response
```
### Example Usage: single

<!-- UsageSnippet language="csharp" operationID="shipmentDispatch" method="post" path="/shipment" example="single" -->
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
    Options = Options.CreateShipmentOptions(
        new ShipmentOptions() {
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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 415, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Documents

Retrieve a shipment document using the shipment ID and document type. Available documents include dispatch confirmations, envelope previews, EPO certificate visualizations in PDF format and EPO certificates in XML format. Availability depends on the document type and shipment state.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Price

Calculate shipment prices for up to **50 recipients** using their addresses or Address Book identifiers, documents and optional shipment settings. For larger batches, split the operation into multiple calls. Check each recipient result to determine whether pricing succeeded.

### Example Usage: advanced_config

<!-- UsageSnippet language="csharp" operationID="shipmentPrice" method="post" path="/shipment/price" example="advanced_config" -->
```csharp
using Postivo;
using Postivo.Models.Components;

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
    Documents = ShipmentDocuments.CreateDocuments(
        Documents.CreateDocumentPdf(
            new DocumentPdf() {
                FileStream = "<document content encoded to base64>",
                FileName = "document.pdf",
            }
        )
    ),
    Options = Options.CreateShipmentOptions(
        new ShipmentOptions() {
            PredefinedConfigId = 2670,
            InlineConfig = InlineConfigUnion.CreateInlineConfig(
                new InlineConfig() {
                    CarrierId = 4,
                    ServiceId = 16,
                    PaperId = 1,
                    ColorPrint = true,
                    DuplexPrint = false,
                    EnvelopeId = 454,
                    EnvelopeColorPrint = true,
                }
            ),
            SenderId = 1,
        }
    ),
};

var res = await sdk.Shipments.PriceAsync(req);

// handle response
```
### Example Usage: multi

<!-- UsageSnippet language="csharp" operationID="shipmentPrice" method="post" path="/shipment/price" example="multi" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Shipment req = new Shipment() {
    Recipients = ShipmentRecipients.CreateArrayOfRecipients(
        new List<Recipients>() {
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
            ),
            Recipients.CreateRecipientInline(
                new RecipientInline() {
                    Name = "Andrzej Kowalski",
                    Address = "ul. Przykładowa 45/321",
                    PostCode = "34-001",
                    City = "Kraków",
                    PhoneNumber = "+48999888777",
                    CustomId = "my-id-1113",
                }
            ),
        }
    ),
    Documents = ShipmentDocuments.CreateDocuments(
        Documents.CreateDocumentPdf(
            new DocumentPdf() {
                FileStream = "<document content encoded to base64>",
                FileName = "document.pdf",
            }
        )
    ),
    Options = Options.CreateShipmentOptions(
        new ShipmentOptions() {
            PredefinedConfigId = 2670,
        }
    ),
};

var res = await sdk.Shipments.PriceAsync(req);

// handle response
```
### Example Usage: single

<!-- UsageSnippet language="csharp" operationID="shipmentPrice" method="post" path="/shipment/price" example="single" -->
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
    Options = Options.CreateShipmentOptions(
        new ShipmentOptions() {
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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 415, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |