# DocumentPdf

PDF document payload.


## Fields

| Field                                           | Type                                            | Required                                        | Description                                     | Example                                         |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `FileStream`                                    | *string*                                        | :heavy_check_mark:                              | Base64-encoded PDF content.                     | <file content in base64 format>                 |
| `FileName`                                      | *string*                                        | :heavy_minus_sign:                              | Optional file name for identification purposes. | document1.pdf                                   |