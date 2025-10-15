# Senders
(*Senders*)

## Overview

### Available Operations

* [List](#list) - List senders
* [Add](#add) - Add a new sender
* [Delete](#delete) - Delete a sender
* [Verify](#verify) - Verify sender

## List

Retrieve the list of allowed senders defined in your account. Senders are registered in your account and must be verified and activated before use. Activated senders have `active: true` property and can be used to send shipments. Inactive senders are also returned (`active: false`), but cannot be used until activated.

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
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Add

Create a new sender on your account. The request must contain a `Sender` object. To prevent fraud, all additional senders are verified by mailing a verification code to the sender’s address. Complete the verification using the `verifySender` method. Verified senders have `active: true` and can be used to send shipments. Inactive senders are also returned (`active: false`), but cannot be used until verification is completed.

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
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Delete

Remove a sender from your account by `id`. Pass the sender’s `id` parameter to remove it. The sender is deleted immediately.

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
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Verify

Verify a sender to activate it. After adding a new sender, a letter containing a verification code is mailed to the sender’s address. Provide this code to complete verification.

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
| Postivo.Models.Errors.ErrorResponse | 404                                 | application/json                    |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |