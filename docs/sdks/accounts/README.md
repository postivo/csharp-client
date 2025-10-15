# Accounts
(*Accounts*)

## Overview

### Available Operations

* [Get](#get) - Retrieve account details
* [GetSubaccount](#getsubaccount) - Get subaccount details

## Get

Retrieve the current account balance and other account details. You can also check the account limit and whether the account is a **main** account. Main accounts have unrestricted privileges and, via the [User Panel](https://panel.postivo.pl), you can create as many subaccounts as needed.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getAccountDetails" method="get" path="/account" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Accounts.GetAsync();

// handle response
```

### Response

**[GetAccountDetailsResponse](../../Models/Requests/GetAccountDetailsResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 403, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## GetSubaccount

Check the account balance and other details, such as the subcredit balance of a subaccount. Subaccounts are additional users who can access your account’s services and data. You can restrict access levels and set privileges for subaccounts in the [User Panel](https://panel.postivo.pl).

Provide the full subaccount login to access its data.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getSubaccountDetails" method="get" path="/account/{user_login}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.Accounts.GetSubaccountAsync(userLogin: "some-login");

// handle response
```

### Parameters

| Parameter                                                  | Type                                                       | Required                                                   | Description                                                | Example                                                    |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `UserLogin`                                                | *string*                                                   | :heavy_check_mark:                                         | Login of the subaccount (user) for which to retrieve data. | some-login                                                 |

### Response

**[GetSubaccountDetailsResponse](../../Models/Requests/GetSubaccountDetailsResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |