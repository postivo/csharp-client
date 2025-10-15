# AddContactResponse


## Fields

| Field                                                                       | Type                                                                        | Required                                                                    | Description                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `HttpMeta`                                                                  | [HTTPMetadata](../../Models/Components/HTTPMetadata.md)                     | :heavy_check_mark:                                                          | N/A                                                                         |
| `ContactResponse`                                                           | [ContactResponse](../../Models/Components/ContactResponse.md)               | :heavy_minus_sign:                                                          | The request was processed successfully (contact added).                     |
| `ErrorResponse`                                                             | [Models.Components.ErrorResponse](../../Models/Components/ErrorResponse.md) | :heavy_minus_sign:                                                          | Invalid request.                                                            |
| `Headers`                                                                   | Dictionary<String, List<*string*>>                                          | :heavy_check_mark:                                                          | N/A                                                                         |