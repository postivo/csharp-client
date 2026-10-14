# StatusDetails

Details of a single shipment and its status events


## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `ShipmentDetails`                                             | [ShipmentDetails](../../Models/Components/ShipmentDetails.md) | :heavy_check_mark:                                            | Single shipment details                                       |
| `StatusEvents`                                                | List<[StatusEvent](../../Models/Components/StatusEvent.md)>   | :heavy_check_mark:                                            | List of status events for the shipment.                       |