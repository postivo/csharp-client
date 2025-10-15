# PingResponse

Ping response.


## Fields

| Field                                                                          | Type                                                                           | Required                                                                       | Description                                                                    | Example                                                                        |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `Status`                                                                       | *string*                                                                       | :heavy_minus_sign:                                                             | API service status: OK (available), ERR (unavailable).                         | OK                                                                             |
| `Version`                                                                      | *string*                                                                       | :heavy_minus_sign:                                                             | Current API version.                                                           | 1.0                                                                            |
| `Sandbox`                                                                      | *bool*                                                                         | :heavy_minus_sign:                                                             | Indicates whether the connection was established to the test system (SANDBOX). | false                                                                          |