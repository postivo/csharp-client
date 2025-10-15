<!-- Start SDK Example Usage [usage] -->
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