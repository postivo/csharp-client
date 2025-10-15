# AccountResponse

Account details, including balance and limits.


## Fields

| Field                                                 | Type                                                  | Required                                              | Description                                           | Example                                               |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| `Login`                                               | *string*                                              | :heavy_minus_sign:                                    | User login.                                           | some_login                                            |
| `AccountType`                                         | [AccountType](../../Models/Components/AccountType.md) | :heavy_minus_sign:                                    | Account type.                                         | PRE-PAID                                              |
| `Limit`                                               | *float*                                               | :heavy_minus_sign:                                    | Account limit.                                        | 0                                                     |
| `Credit`                                              | *float*                                               | :heavy_minus_sign:                                    | Current account balance.                              | 130.44                                                |
| `Subcredit`                                           | *float*                                               | :heavy_minus_sign:                                    | Subaccount credit balance; null if unlimited.         | 65.32                                                 |
| `Currency`                                            | *string*                                              | :heavy_minus_sign:                                    | Account currency.                                     | PLN                                                   |
| `Name`                                                | *string*                                              | :heavy_minus_sign:                                    | User full name.                                       | Andrzej Nowak                                         |
| `IsMain`                                              | *bool*                                                | :heavy_minus_sign:                                    | Indicates whether this is the main account.           | true                                                  |