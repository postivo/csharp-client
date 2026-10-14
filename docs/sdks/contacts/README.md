# AddressBook.Contacts

## Overview

### Available Operations

* [List](#list) - List contacts
* [Add](#add) - Add a new contact
* [Get](#get) - Retrieve contact details
* [Update](#update) - Update a contact
* [Delete](#delete) - Delete a contact
* [RemoveFromGroup](#removefromgroup) - Remove a contact from a group
* [AddToGroup](#addtogroup) - Add a contact to a group

## List

Retrieve a paginated list of contacts defined in your account's **Address Book**. An Address Book without contacts returns an empty list.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listContacts" method="get" path="/contacts" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.ListAsync(
    page: 1,
    limit: 10
);

// handle response
```

### Parameters

| Parameter               | Type                    | Required                | Description             | Example                 |
| ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- |
| `Page`                  | *long*                  | :heavy_minus_sign:      | Page number of results  | 1                       |
| `Limit`                 | *long*                  | :heavy_minus_sign:      | Results limit per page. | 10                      |

### Response

**[ListContactsResponse](../../Models/Requests/ListContactsResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Add

Create a new contact in your account's **Address Book**. An optional external (custom) ID must be unique within the Address Book.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="addContact" method="post" path="/contacts" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Contact req = new Contact() {
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
};

var res = await sdk.AddressBook.Contacts.AddAsync(req);

// handle response
```

### Parameters

| Parameter                                     | Type                                          | Required                                      | Description                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `request`                                     | [Contact](../../Models/Components/Contact.md) | :heavy_check_mark:                            | The request object to use for the request.    |

### Response

**[AddContactResponse](../../Models/Requests/AddContactResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 409, 415, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Get

Get the details of an Address Book contact using its system ID.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getContactById" method="get" path="/contacts/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.GetAsync(id: 14);

// handle response
```

### Parameters

| Parameter                     | Type                          | Required                      | Description                   | Example                       |
| ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
| `Id`                          | *long*                        | :heavy_check_mark:            | Global contact `id` to fetch. | 14                            |

### Response

**[GetContactByIdResponse](../../Models/Requests/GetContactByIdResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 404, 4XX                       | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Update

Update an Address Book contact using its system ID. Submitting unchanged details leaves the contact unchanged.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateContact" method="put" path="/contacts/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using System.Collections.Generic;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.UpdateAsync(
    id: 14,
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

| Parameter                                     | Type                                          | Required                                      | Description                                   | Example                                       |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `Id`                                          | *long*                                        | :heavy_check_mark:                            | ID of the contact to update.                  | 14                                            |
| `Contact`                                     | [Contact](../../Models/Components/Contact.md) | :heavy_check_mark:                            | Updated contact details.                      |                                               |

### Response

**[UpdateContactResponse](../../Models/Requests/UpdateContactResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 409, 415, 4XX        | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Delete

Remove an Address Book contact using its system ID.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteContact" method="delete" path="/contacts/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.DeleteAsync(id: 14);

// handle response
```

### Parameters

| Parameter                      | Type                           | Required                       | Description                    | Example                        |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| `Id`                           | *long*                         | :heavy_check_mark:             | Global contact `id` to remove. | 14                             |

### Response

**[DeleteContactResponse](../../Models/Requests/DeleteContactResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## RemoveFromGroup

Remove a contact from an Address Book group using the contact and group system IDs. The contact remains in the Address Book.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="removeContactFromGroup" method="delete" path="/contacts/{id}/group/{group_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.RemoveFromGroupAsync(
    id: 35,
    groupId: 656
);

// handle response
```

### Parameters

| Parameter                                     | Type                                          | Required                                      | Description                                   | Example                                       |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `Id`                                          | *long*                                        | :heavy_check_mark:                            | Global contact `id` to detach from the group. | 35                                            |
| `GroupId`                                     | *long*                                        | :heavy_check_mark:                            | Group `id` to detach from the contact.        | 656                                           |

### Response

**[RemoveContactFromGroupResponse](../../Models/Requests/RemoveContactFromGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## AddToGroup

Assign a contact to an Address Book group using the contact and group system IDs. Both the contact and the group must exist in your Address Book.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="addContactToGroup" method="patch" path="/contacts/{id}/group/{group_id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Contacts.AddToGroupAsync(
    id: 35,
    groupId: 656
);

// handle response
```

### Parameters

| Parameter                                 | Type                                      | Required                                  | Description                               | Example                                   |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| `Id`                                      | *long*                                    | :heavy_check_mark:                        | Global contact `id` to add to the group.  | 35                                        |
| `GroupId`                                 | *long*                                    | :heavy_check_mark:                        | Group `id` to associate with the contact. | 656                                       |

### Response

**[AddContactToGroupResponse](../../Models/Requests/AddContactToGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 401, 405                            | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 400, 403, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |