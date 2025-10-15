# Groups
(*AddressBook.Groups*)

## Overview

### Available Operations

* [List](#list) - List groups
* [Add](#add) - Add a new group
* [Get](#get) - Retrieve group details
* [Update](#update) - Update a group
* [Delete](#delete) - Delete a group

## List

Retrieve the full list of groups defined in your account’s Address Book.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listGroups" method="get" path="/groups" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Groups.ListAsync();

// handle response
```

### Response

**[ListGroupsResponse](../../Models/Requests/ListGroupsResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Add

Create a new contact group in your account’s Address Book.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="addGroup" method="post" path="/groups" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

Group req = new Group() {
    Name = "my-group",
    Description = "This is a group for school contacts",
};

var res = await sdk.AddressBook.Groups.AddAsync(req);

// handle response
```

### Parameters

| Parameter                                  | Type                                       | Required                                   | Description                                |
| ------------------------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------------ |
| `request`                                  | [Group](../../Models/Components/Group.md)  | :heavy_check_mark:                         | The request object to use for the request. |

### Response

**[AddGroupResponse](../../Models/Requests/AddGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Get

Get the details of a single group from your Address Book by its `id` (returned when the group was created).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getGroupById" method="get" path="/groups/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Groups.GetAsync(id: 194);

// handle response
```

### Parameters

| Parameter          | Type               | Required           | Description        | Example            |
| ------------------ | ------------------ | ------------------ | ------------------ | ------------------ |
| `Id`               | *long*             | :heavy_check_mark: | Group id to fetch  | 194                |

### Response

**[GetGroupByIdResponse](../../Models/Requests/GetGroupByIdResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 404, 4XX                  | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Update

Update a group’s details by ID.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateGroup" method="put" path="/groups/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Groups.UpdateAsync(
    id: 14,
    groupP: new Group() {
        Name = "my-group",
        Description = "This is a group for school contacts",
    }
);

// handle response
```

### Parameters

| Parameter                                 | Type                                      | Required                                  | Description                               | Example                                   |
| ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- | ----------------------------------------- |
| `Id`                                      | *long*                                    | :heavy_check_mark:                        | Group `id` to update.                     | 14                                        |
| `Group`                                   | [Group](../../Models/Components/Group.md) | :heavy_check_mark:                        | A `Group` object with the updated fields. |                                           |

### Response

**[UpdateGroupResponse](../../Models/Requests/UpdateGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |

## Delete

Remove a group from your account’s Address Book by `ID`. Pass the group’s `id` to remove it. The group is deleted immediately from the Address Book.

If you also want to remove contacts that belong to this group, set the parameter `contacts` to `delete`. The default is `contacts: detach`, which detaches contacts from the removed group but leaves them in the Address Book.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteGroup" method="delete" path="/groups/{id}" -->
```csharp
using Postivo;
using Postivo.Models.Components;
using Postivo.Models.Requests;

var sdk = new Client(bearer: "<YOUR API ACCESS TOKEN>");

var res = await sdk.AddressBook.Groups.DeleteAsync(
    id: 876,
    contacts: ContactHandling.Detach
);

// handle response
```

### Parameters

| Parameter                                                   | Type                                                        | Required                                                    | Description                                                 | Example                                                     |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `Id`                                                        | *long*                                                      | :heavy_check_mark:                                          | Group `id` to remove.                                       | 876                                                         |
| `Contacts`                                                  | [ContactHandling](../../Models/Requests/ContactHandling.md) | :heavy_minus_sign:                                          | How to handle contacts that belong to the group.            |                                                             |

### Response

**[DeleteGroupResponse](../../Models/Requests/DeleteGroupResponse.md)**

### Errors

| Error Type                          | Status Code                         | Content Type                        |
| ----------------------------------- | ----------------------------------- | ----------------------------------- |
| Postivo.Models.Errors.ErrorResponse | 400, 401, 403, 404, 4XX             | application/problem+json            |
| Postivo.Models.Errors.ErrorResponse | 5XX                                 | application/problem+json            |