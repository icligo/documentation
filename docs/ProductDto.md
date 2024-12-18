## Properties

| Name              | Type                                      | Description                                                     | Notes                                                                        |
|-------------------|-------------------------------------------|-----------------------------------------------------------------|------------------------------------------------------------------------------|
| **type**          | [**ProductTypeEnum**](ProductTypeEnum.md) | Type of the product.                                            | [required]                                                                   |
| **name**          | **String**                                | Name of the product.                                            | [required]                                                                   |
| **location**      | **String**                                | Location of the product.                                        | [required for: ACCOMMODATION, TRANSFER, ACTIVITY, and EVENT]                 |
| **duration**      | **String**                                | Duration of the product/service.                                | [required for: ACTIVITY]                                                     |
| **code**          | **String**                                | Unique product code.                                            | [optional]                                                                   |
| **transport**     | [**TransportEnum**](TransportEnum.md)     | Type of transport associated with the product, if applicable.   | [required for: TRANSFER]                                                     |
| **checkin**       | **Date**                                  | Check-in date of the product, formatted as a string.            | [required for: FLIGHT, ACCOMMODATION, CRUISE, TRANSFER, ACTIVITY, and EVENT] |
| **checkout**      | **Date**                                  | Check-out date of the product, formatted as a string.           | [required for: ACCOMMODATION, TRANSFER, ACTIVITY, and EVENT]                 |
| **date**          | **Date**                                  | Date of the product activity or service, formatted as a string. | [optional]                                                                   |
| **price**         | **Number**                                | Price of the product.                                           | [required for: INSURANCE]                                                    |
| **detail**        | [**DetailDto**](DetailDto.md)             |                                                                 | [required for: FLIGHT, ACCOMMODATION, CRUISE, and TRANSFER]                  |
| **importantInfo** | **String**                                | String with Important information in plain text.                | [required]                                                                   |

### Examples of products

=== "FLIGHT"

```json 
{
  "type": "FLIGHT",
  "name": "TAP air PORTUGAL",
  "checkin": "2024-12-04",
  "importantInfo": "Important notes ...",
  "detail": {
    "flightNumber": "1234546",
    "departure": "2024-12-05",
    "arrival": "2024-12-20",
    "departureTime": "10:00",
    "arrivalTime": "16:00",
    "departureAirport": "OPO",
    "arrivalAirport": "IST",
    "departureCity": "Porto",
    "arrivalCity": "Istanbul",
    "departureCountry": "Portugal",
    "arrivalCountry": "Turkey",
    "baggage": "1",
    "duration": "4h"
  }
}
```

=== "ACCOMMODATION"

```json 
{
  "type": "ACCOMMODATION",
  "name": "Hotel's name",
  "location": "Istanbul",
  "checkin": "2024-12-05",
  "checkout": "2024-12-20",
  "importantInfo": "Important notes ...",
  "detail": {
    "night": 9,
    "roomType": "OCEAN_VIEW",
    "regime": "all-inclusive"
  }
}
```

=== "CRUISE"

```json 
{
  "type": "CRUISE",
  "name": "cruise name",
  "checkin": "2024-12-15",
  "importantInfo": "Important notes ...",
  "detail": {
    "night": 9,
    "roomType": "OCEAN_VIEW",
    "regime": "all-inclusive",
    "circuit": [
      {
        "checkin": "2024-12-11T11:03:42.501+00:00",
        "checkout": "2024-12-11T11:03:42.501+00:00",
        "location": "Turkey"
      },
      {
        "checkin": "2024-12-20T11:03:42.501+00:00",
        "checkout": "2024-12-20T11:03:42.501+00:00",
        "location": "Turkey"
      }
    ]
  }
}
```

=== "TRANSFER"

```json 
{
  "type": "TRANSFER",
  "name": "BUS 309",
  "location": "Istanbul",
  "transport": "BUS",
  "checkin": "2024-12-20",
  "checkout": "2024-12-20",
  "importantInfo": "Important notes ...",
  "detail": {
    "provider": "Istanbul Transfers",
    "reception": "Crowne Plaza: Istanbul - Old City",
    "receptionTime": "2024-09-20T16:00",
    "destinationTime": "2024-09-20T16:15",
    "destination": "Istanbul Airport"
  }
}
```

=== "ACTIVITY"

```json 
{
  "type": "ACTIVITY",
  "name": "Activity's name",
  "location": "Istanbul",
  "duration": "3h",
  "checkin": "2024-12-15",
  "checkout": "2024-12-15",
  "importantInfo": "Important notes ..."
}
```

=== "INSURANCE"

```json 
{
  "type": "INSURANCE",
  "name": "Insurance's Name",
  "price": 12,
  "importantInfo": "Important notes ..."
}
```

=== "EVENT"

```json 
{
  "type": "EVENT",
  "name": "Event's name",
  "location": "Istanbul",
  "checkin": "2021-12-01",
  "checkout": "2021-12-10",
  "importantInfo": "Important notes ..."
}
```