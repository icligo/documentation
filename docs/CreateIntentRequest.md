# CreateIntentRequest

## Properties

| Name                        | Type                                                | Description                                                                                                                                                         | Notes      |
|-----------------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **clientId**                | **String**                                          | Unique client identifier. Identifies the client that is making the request, in this case it&#x27;syour company/merchant ID agreed at the beginning of the contract. | [required] |
| **userId**                  | **String**                                          | The user ID associated with the payment.                                                                                                                            | [required] |
| **userName**                | **String**                                          | The User name.                                                                                                                                                      | [required] |
| **userEmail**               | **String**                                          | The User e-mail.                                                                                                                                                    | [required] |
| **userContact**             | **String**                                          | The User contact.                                                                                                                                                   | [required] |
| **productId**               | **String**                                          | The ID of the product being purchased.                                                                                                                              | [required] |
| **intentType**              | [**IntentTypeEnum**](IntentTypeEnum.md)             | Type of the product.                                                                                                                                                | [required] |
| **resume**                  | [**ResumeDto**](ResumeDto.md)                       |                                                                                                                                                                     | [required] |
| **products**                | [**[ProductDto]**](ProductDto.md)                   | A list of products associated with the payment.                                                                                                                     | [required] |
| **currency**                | **String**                                          | Currency code for the payment.                                                                                                                                      | [required] |
| **company**                 | **String**                                          | Company making the payment request.                                                                                                                                 | [required] |
| **microsite**               | **String**                                          | The microsite making the payment request.                                                                                                                           | [required] |
| **country**                 | **String**                                          | Country where the payment is being made.                                                                                                                            | [required] |
| **amount**                  | **Number**                                          | The amount to be charged.                                                                                                                                           | [required] |
| **totalAmountService**      | **Number**                                          | Total amount of the service. Obs: This is NOT the value to be charged, it's for visualization purpose that covers all the service's value.                          | [required] |
| **successUrl**              | **String**                                          | The success url to redirect the user after a successful payment.                                                                                                    | [optional] |
| **failureUrl**              | **String**                                          | The failure url to redirect the user after a failure on the payment.                                                                                                | [optional] |
| **manualCapture**           | **Boolean**                                         | If the payment it will be on capture or manual form.                                                                                                                | [required] |
| **expirationDate**          | **Date**                                            | The expiration date of the intent.                                                                                                                                  | [optional] |
| **cancellationFees**        | [**[CancellationFeesDto]**](CancellationFeesDto.md) | List of cancellation fees                                                                                                                                           | [required] |
| **cancellationFeesStrings** | **String**                                          | List of cancellation fees on plain                                                                                                                                  | [required] |
| **ideaId**                  | **String**                                          | Idea identifier.                                                                                                                                                    | [required] |

## Example 

=== "Only Cruise"

```json
{
  "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
  "userEmail": "joedoe@email.com",
  "userContact": "+351 910 000 000",
  "userName": "Joe Doe",
  "cancellationFees": [
    {
      "limitDate": "2000-12-12",
      "price": "10.00"
    }
  ],
  "cancellationFeesStrings": [
    "Non-refundable.",
    "Refundable until 12-12-2000 with a fee of 10.00.",
    "string ...."
  ],
  "resume": {
    "owner": "Bob Smith",
    "clients": [
      {
        "name": "Nome 1",
        "email": "email@email.com",
        "dateOfBirth": "2000-10-10",
        "children": false
      },
      {
        "name": "Nome 2",
        "email": "email2@email.com",
        "dateOfBirth": "2000-10-10",
        "children": false
      }
    ]
  },
  "intentType": "BOOKING",
  "productId": "my-product-id-123",
  "products": [
    {
      "type": "CRUISE",
      "name": "cruise name",
      "checkin": "2024-12-24",
      "checkout": "2021-12-25",
      "location": "Istanbul",
      "importantInfo": "Important notes ...",
      "detail": {
        "night": 2,
        "roomType": "Oceanview",
        "regime": "all-inclusive",
        "circuit": [
          {
            "checkin": "2024-12-24T11:03:42.501+00:00",
            "checkout": "2024-12-24T11:03:42.501+00:00",
            "location": "Turkey"
          },
          {
            "checkin": "2024-12-25T11:03:42.501+00:00",
            "checkout": "2024-12-25T11:03:42.501+00:00",
            "location": "Turkey"
          }
        ]
      }
    }
  ],
  "company": "icligo.pt",
  "currency": "EUR",
  "microsite": "icligo.pt",
  "country": "pt",
  "manualCapture": true,
  "successUrl": "https://success.com",
  "failureUrl": "https://failure.com",
  "ideaId": "15847300",
  "amount": 100.0,
  "totalAmountService": 2500.00,
  "expirationDate": "2024-12-31T11:43:00.000Z"
}
```

=== "With All Products"

```json
{
  "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
  "userEmail": "joedoe@email.com",
  "userContact": "+351 910 000 000",
  "userName": "Joe Doe",
  "cancellationFees": [
    {
      "limitDate": "2000-12-12",
      "price": "10.00"
    }
  ],
  "cancellationFeesStrings": [
    "Non-refundable.",
    "Refundable until 12-12-2000 with a fee of 10.00.",
    "string ...."
  ],
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
  "intentType": "BOOKING",
  "productId": "my-product-id-123",
  "products": [
    {
      "type": "BOOKING",
      "name": "Product XYZ",
      "location": "Location X",
      "duration": "10 Minutes",
      "code": "PRD12345",
      "transport": "CAR",
      "checkin": "2024-09-24T16:46:42.411Z",
      "checkout": "2024-09-24T16:46:42.411Z",
      "date": "2024-09-24T16:46:42.411Z",
      "price": 500,
      "importantInfo": "Important notes ...",
      "detail": {
        "night": 3,
        "roomType": "Suite",
        "regime": "Half board",
        "flightNumber": "FL123",
        "departure": "2024-09-24T16:46:42.411Z",
        "arrival": "2024-09-24T16:46:42.411Z",
        "departureTime": "2024-09-24T16:46:42.411Z",
        "arrivalTime": "string",
        "departureAirport": "JFK",
        "arrivalAirport": "LHR",
        "departureCity": "New York",
        "arrivalCity": "London",
        "departureCountry": "US",
        "arrivalCountry": "UK",
        "baggage": "string",
        "duration": "string",
        "provider": "Airline XYZ",
        "reception": "string",
        "receptionTime": "2024-09-24T16:46:42.411Z",
        "destinationTime": "2024-09-24T16:46:42.411Z",
        "destination": "string",
        "circuit": [
          {
            "checkin": "2024-09-24T16:46:42.411Z",
            "checkout": "2024-09-24T16:46:42.411Z",
            "location": "string"
          }
        ],
        "stopovers": [
          {
            "departure": "2024-09-24T16:46:42.411Z",
            "arrival": "2024-09-24T16:46:42.411Z",
            "departureTime": "2024-09-24T16:46:42.411Z",
            "arrivalTime": "2024-09-24T16:46:42.411Z",
            "departureAirport": "string",
            "arrivalAirport": "string",
            "departureCity": "string",
            "arrivalCity": "string",
            "departureCountry": "string",
            "arrivalCountry": "string",
            "duration": "2H"
          }
        ]
      }
    },
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
    },
    {
      "type": "CRUISE",
      "name": "cruise name",
      "checkin": "2024-12-15",
      "importantInfo": "Important notes ...",
      "detail": {
        "night": 9,
        "roomType": "Oceanview",
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
    },
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
      "importantInfo": "Important notes ...",
      "detail": {
        "night": 9,
        "roomType": "Oceanview",
        "regime": "all-inclusive"
      }
    }
  ],
  "company": "icligo.pt",
  "currency": "EUR",
  "microsite": "icligo.pt",
  "country": "pt",
  "manualCapture": true,
  "successUrl": "https://success.com",
  "failureUrl": "https://failure.com",
  "ideaId": "15847300",
  "amount": 100.0,
  "totalAmountService": 2500.00,
  "expirationDate": "2027-12-31T11:43:00.000Z"
}
```
