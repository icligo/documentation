# ExternalPaymentDto

## Properties

| Name                   | Type                                     | Description                                                                                                                                | Notes |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------|
| **id**                 | **String**                               | Unique identifier for the payment intent.                                                                                                  | -     |
| **clientId**           | **String**                               | Unique client identifier.                                                                                                                  | -     |
| **userId**             | **String**                               | User/Customer identifier who initiated the payment.                                                                                        | -     |
| **service**            | **String**                               | Service associated with the payment.                                                                                                       | -     |
| **serviceDescription** | **String**                               | Detailed description of the service.                                                                                                       | -     |
| **productId**          | **String**                               | Product identifier related to the payment.                                                                                                 | -     |
| **intentType**         | [**IntentTypeEnum**](ProductTypeEnum.md) | Type of the product for which the intent is being made.                                                                                    | -     |
| **resume**             | [**ResumeDto**](ResumeDto.md)            | Resume of the service.                                                                                                                     | -     |
| **products**           | [**ProductDto**](ProductDto.md)          | List of products associated with this payment.                                                                                             | -     |
| **company**            | **String**                               | Company associated with the payment.                                                                                                       | -     |
| **microsite**          | **String**                               | Microsite used for making the payment.                                                                                                     | -     |
| **country**            | **String**                               | Country where the payment is being made.                                                                                                   | -     |
| **currency**           | **String**                               | Currency code for the payment. Must respect the ISO 4217 and be upper case.                                                                | -     |
| **createdBy**          | **String**                               | Username of the person who created the payment.                                                                                            | -     |
| **state**              | [**StateEnum**](StateEnum.md)            | Current state of the payment.                                                                                                              | -     |
| **amount**             | **Number**                               | Total amount of the order.                                                                                                                 | -     |
| **totalAmountService** | **Number**                               | Total amount of the service. Obs: This is NOT the value to be charged, it's for visualization purpose that covers all the service's value. | -     | 
| **capturedAmount**     | **Number**                               | Amount captured.                                                                                                                           | -     |
| **authorizedAmount**   | **Number**                               | Amount authorized to be captured.                                                                                                          | -     |
| **refundedAmount**     | **Number**                               | Amount refunded.                                                                                                                           | -     |
| **manualCapture**      | **Boolean**                              | If the payment is on capture or manual form.                                                                                               | -     |
| **captureDetails**     | [**CaptureDetail**](CaptureDetail.md)    | Details of the captures made for the payment.                                                                                              | -     |
| **refundDetails**      | [**RefundDetail**](RefundDetail.md)      | Details of any refunds made for the payment.                                                                                               | -     |
| **expirationDate**     | **Date**                                 | Expiration date of the payment.                                                                                                            | -     |
| **successUrl**         | **String**                               | The success url to redirect the user after a successful payment.                                                                           | -     |
| **failureUrl**         | **String**                               | The failure url to redirect the user after a failure on the payment.                                                                       | -     |
| **testMode**           | **Boolean**                              | If the payment it was created using a account.                                                                                             | -     |                                                                                                                                            |            |

## Example

```json
{
  "id": "b91c35cc-db74-4663-a491-bed750686faa",
  "clientId": "travel-c-app-test",
  "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
  "productId": "my-product-id-123",
  "intentType": "BOOKING",
  "resume": {
    "owner": "Bob Smith",
    "clients": [
      {
        "name": "Name 1",
        "email": "email@email.com",
        "dateOfBirth": "2000-10-10",
        "children": false
      },
      {
        "name": "Name 2",
        "email": "email2@email.com",
        "dateOfBirth": "2000-10-10",
        "children": false
      }
    ]
  },
  "products": [
    {
      "type": "FLIGHT",
      "name": "TAP air PORTUGAL",
      "checkin": "2024-12-04",
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
      },
      "importantInfo": "Important notes ..."
    },
    {
      "type": "CRUISE",
      "name": "cruise name",
      "checkin": "2024-12-15",
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
      },
      "importantInfo": "Important notes ..."
    },
    {
      "type": "TRANSFER",
      "name": "BUS 309",
      "location": "Istanbul",
      "transport": "BUS",
      "checkin": "2024-12-20",
      "checkout": "2024-12-20",
      "detail": {
        "provider": "Istanbul Transfers",
        "reception": "Crowne Plaza: Istanbul - Old City",
        "receptionTime": "2024-09-20T16:00",
        "destinationTime": "2024-09-20T16:15",
        "destination": "Istanbul Airport"
      },
      "importantInfo": "Important notes ..."
    },
    {
      "type": "ACTIVITY",
      "name": "Activity's name",
      "location": "Istanbul",
      "duration": "3h",
      "checkin": "2024-12-15",
      "checkout": "2024-12-15",
      "importantInfo": "Important notes ..."
    },
    {
      "type": "INSURANCE",
      "name": "Seguro XYZ",
      "price": 12,
      "importantInfo": "Important notes ..."
    },
    {
      "type": "EVENT",
      "name": "Event's name",
      "location": "Istanbul",
      "checkin": "2021-12-01",
      "checkout": "2021-12-10",
      "importantInfo": "Important notes ..."
    },
    {
      "type": "ACCOMMODATION",
      "name": "Hotel's name",
      "location": "Istanbul",
      "checkin": "2024-12-05",
      "checkout": "2024-12-20",
      "detail": {
        "night": 9,
        "roomType": "OCEAN_VIEW",
        "regime": "all-inclusive"
      },
      "importantInfo": "Important notes ..."
    }
  ],
  "company": "icligo.pt",
  "microsite": "icligo.pt",
  "country": "pt",
  "currency": "EUR",
  "state": "CREATED",
  "amount": 100.0,
  "totalAmountService": 2500.00,
  "capturedAmount": 0,
  "authorizedAmount": 0,
  "refundedAmount": 0,
  "manualCapture": true,
  "captureDetails": [],
  "refundDetails": [],
  "successUrl": "https://success.com",
  "failureUrl": "https://failure.com",
  "testMode": true
}
```