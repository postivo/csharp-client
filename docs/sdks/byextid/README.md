# AddressBook.Contacts.ByExtId

## Overview

### Available Operations

* [Get](#get) - Retrieve contact details by EXT_ID
* [Update](#update) - Update a contact by EXT_ID
* [Delete](#delete) - Delete a contact by EXT_ID
* [RemoveFromGroup](#removefromgroup) - Remove a contact from a group by EXT_ID
* [AddToGroup](#addtogroup) - Add a contact to a group by EXT_ID

## Get

Get the details of an Address Book contact using its external (custom) ID, assigned when the contact was created.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 404, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Update

Update an Address Book contact using its external (custom) ID, assigned when the contact was created. Submitting unchanged details leaves the contact unchanged.

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
| `Contact`                                      | [Contact](../../Models/Components/Contact.md)  | :heavy_check_mark:                             | Updated contact details.                       |                                                |

### Response

**[UpdateContactByExternalIdResponse](../../Models/Requests/UpdateContactByExternalIdResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 409, 415, 4XX        | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Delete

Remove an Address Book contact using its external (custom) ID, assigned when the contact was created.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## RemoveFromGroup

Remove a contact from an Address Book group using the contact's external (custom) ID and the group's system ID. The contact remains in the Address Book.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## AddToGroup

Assign a contact to an Address Book group using the contact's external (custom) ID and the group's system ID. Both the contact and the group must exist in your Address Book.

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
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |