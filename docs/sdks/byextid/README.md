# ByExtId
(*AddressBook.Contacts.ByExtId*)

## Overview

### Available Operations

* [Get](#get) - Retrieve contact details by EXT_ID
* [Update](#update) - Update a contact by EXT_ID
* [Delete](#delete) - Delete a contact by EXT_ID
* [RemoveFromGroup](#removefromgroup) - Remove a contact from a group by EXT_ID
* [AddToGroup](#addtogroup) - Add a contact to a group by EXT_ID

## Get

Get the details of a contact from your Address Book using your external (custom) ID (the value you defined when creating the contact).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getContactByExternalId" method="get" path="/contacts/external/{ext_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.ByExtId.GetAsync(extId: "my-ext-id-44");

// handle response
```

### Parameters

| Parameter                                     | Type                                          | Required                                      | Description                                   | Example                                       |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `ExtId`                                       | *string*                                      | :heavy_check_mark:                            | External (custom) ID of the contact to fetch. | my-ext-id-44                                  |

### Response

**[GetContactByExternalIdResponse](../../Models/Requests/GetContactByExternalIdResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Update

Update a contact by its external (custom) ID - the value you defined when creating the contact.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateContactByExternalId" method="put" path="/contacts/external/{ext_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.ByExtId.UpdateAsync(
    extId: "my-id-2",
    contact: new Contact() {
        Name = "Jan Nowak",
        Name2 = "Firma Testowa Sp. z o.o.",
        Address = "ul. Aleje Jerozolimskie",
        HomeNumber = "31",
        FlatNumber = "2",
        PostCode = "00-999",
        City = "Warszawa",
        PhoneNumber = "+48999999999",
        ExtId = "my-contact-1",
        GroupIds = new List<long>() {
            13,
            534,
        },
    }
);

// handle response
```

### Parameters

| Parameter                                      | Type                                           | Required                                       | Description                                    | Example                                        |
| ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| `ExtId`                                        | *string*                                       | :heavy_check_mark:                             | External (custom) ID of the contact to update. | my-id-2                                        |
| `Contact`                                      | [Contact](../../Models/Components/Contact.md)  | :heavy_check_mark:                             | A `Contact` object with the updated fields.    |                                                |

### Response

**[UpdateContactByExternalIdResponse](../../Models/Requests/UpdateContactByExternalIdResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Delete

Remove a contact from your account by its external (custom) ID - the value defined when the contact was created.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteContactByExternalId" method="delete" path="/contacts/external/{ext_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.ByExtId.DeleteAsync(extId: "my-id-2");

// handle response
```

### Parameters

| Parameter                                      | Type                                           | Required                                       | Description                                    | Example                                        |
| ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| `ExtId`                                        | *string*                                       | :heavy_check_mark:                             | External (custom) ID of the contact to remove. | my-id-2                                        |

### Response

**[DeleteContactByExternalIdResponse](../../Models/Requests/DeleteContactByExternalIdResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## RemoveFromGroup

Remove a contact from a group in your Address Book using the contact’s external (custom) ID. This operation does not delete the contact; it only detaches the contact from the group. Provide the contact’s `ext_id` and the group’s `group_id` parameters to perform the detachment.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="removeContactByExtIdToGroup" method="delete" path="/contacts/external/{ext_id}/group/{group_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.ByExtId.RemoveFromGroupAsync(
    extId: "my-id-1",
    groupId: 656
);

// handle response
```

### Parameters

| Parameter                                                     | Type                                                          | Required                                                      | Description                                                   | Example                                                       |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `ExtId`                                                       | *string*                                                      | :heavy_check_mark:                                            | External (custom) ID of the contact to detach from the group. | my-id-1                                                       |
| `GroupId`                                                     | *long*                                                        | :heavy_check_mark:                                            | Group `id` to detach from the contact.                        | 656                                                           |

### Response

**[RemoveContactByExtIdToGroupResponse](../../Models/Requests/RemoveContactByExtIdToGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 404                                 | application/json                    |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## AddToGroup

Assign a contact to a group using the contact’s external (custom) ID (assigned when creating the contact). If a contact and a group exist in your account, you can add the contact to that group.

Provide the contact’s `ext_id` and the group’s `group_id` parameters to perform the assignment.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="addContactByExtIdToGroup" method="patch" path="/contacts/external/{ext_id}/group/{group_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.ByExtId.AddToGroupAsync(
    extId: "my-id-1",
    groupId: 656
);

// handle response
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ExtId`                                                  | *string*                                                 | :heavy_check_mark:                                       | External (custom) ID of the contact to add to the group. | my-id-1                                                  |
| `GroupId`                                                | *long*                                                   | :heavy_check_mark:                                       | Group `id` to associate with the contact.                | 656                                                      |

### Response

**[AddContactByExtIdToGroupResponse](../../Models/Requests/AddContactByExtIdToGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 404                                 | application/json                    |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |