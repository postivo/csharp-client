# MetadataResponse

Metadata response.


## Fields

| Field                                                                               | Type                                                                                | Required                                                                            | Description                                                                         |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `Carriers`                                                                          | List<[MetadataResponseCarrier](../../Models/Components/MetadataResponseCarrier.md)> | :heavy_minus_sign:                                                                  | List of carriers and their available services.                                      |
| `Papers`                                                                            | List<[Paper](../../Models/Components/Paper.md)>                                     | :heavy_minus_sign:                                                                  | Available paper types.                                                              |
| `EnvelopeTemplates`                                                                 | List<[EnvelopeTemplate](../../Models/Components/EnvelopeTemplate.md)>               | :heavy_minus_sign:                                                                  | Envelope template groups, each containing related templates.                        |
| `StatusCodes`                                                                       | List<[StatusCode](../../Models/Components/StatusCode.md)>                           | :heavy_minus_sign:                                                                  | Available status codes.                                                             |