# PingResponse

Postivo service availability and current API version.


## Fields

| Field                                                                          | Type                                                                           | Required                                                                       | Description                                                                    | Example                                                                        |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `Status`                                                                       | *string*                                                                       | :heavy_minus_sign:                                                             | API service status. A successful ping returns OK.                              | OK                                                                             |
| `Version`                                                                      | *string*                                                                       | :heavy_minus_sign:                                                             | Current API version.                                                           | 1.1.1                                                                          |
| `Sandbox`                                                                      | *bool*                                                                         | :heavy_minus_sign:                                                             | Indicates whether the connection was established to the test system (SANDBOX). | false                                                                          |