# Senders

## Overview

### Available Operations

* [List](#list) - List senders
* [Add](#add) - Add a new sender
* [Delete](#delete) - Delete a sender
* [Verify](#verify) - Verify sender

## List

Retrieve the senders defined in your account. Active, verified senders can be used for shipments. Inactive senders are also included in the list.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listSenders" method="get" path="/senders" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Senders.ListAsync();

// handle response
```

### Response

**[ListSendersResponse](../../Models/Requests/ListSendersResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Add

Create a sender using its address details. Additional senders are verified by mailing a verification code to the sender's address. Complete verification with the received code to activate the sender.

The sender can be created before the verification letter is sent. If sending the letter fails, retrieve the sender list before retrying creation.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="addSender" method="post" path="/senders" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Sender req = new Sender() {
    Name = "Jan Nowak",
    Name2 = "Firma Testowa Sp. z o.o.",
    Address = "ul. Aleje Jerozolimskie",
    HomeNumber = "31",
    FlatNumber = "2",
    PostCode = "00-999",
    City = "Warszawa",
    Country = "PL",
};

var res = await sdk.Senders.AddAsync(req);

// handle response
```

### Parameters

| Parameter                                   | Type                                        | Required                                    | Description                                 |
| ------------------------------------------- | ------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
| `request`                                   | [Sender](../../Models/Components/Sender.md) | :heavy_check_mark:                          | The request object to use for the request.  |

### Response

**[AddSenderResponse](../../Models/Requests/AddSenderResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 409, 415, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Delete

Remove a sender using its system ID. The account's default sender must be retained.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteSender" method="delete" path="/senders/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Senders.DeleteAsync(id: 14);

// handle response
```

### Parameters

| Parameter              | Type                   | Required               | Description            | Example                |
| ---------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- |
| `Id`                   | *long*                 | :heavy_check_mark:     | Sender `id` to remove. | 14                     |

### Response

**[DeleteSenderResponse](../../Models/Requests/DeleteSenderResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 409, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Verify

Activate a sender using the verification code received by mail. The code must match the current verification request, and the sender must still be awaiting verification.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="verifySender" method="patch" path="/senders/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using Postivo.Models.Requests;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Senders.VerifyAsync(
    id: 443,
    requestBody: new VerifySenderRequestBody() {
        VerificationCode = "A345FP73",
    }
);

// handle response
```

### Parameters

| Parameter                                                                   | Type                                                                        | Required                                                                    | Description                                                                 | Example                                                                     |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `Id`                                                                        | *long*                                                                      | :heavy_check_mark:                                                          | ID of the sender to verify.                                                 | 443                                                                         |
| `RequestBody`                                                               | [VerifySenderRequestBody](../../Models/Requests/VerifySenderRequestBody.md) | :heavy_check_mark:                                                          | Verification code received in the letter.                                   |                                                                             |

### Response

**[VerifySenderResponse](../../Models/Requests/VerifySenderResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 409, 415, 4XX        | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |