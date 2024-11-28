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
  "id": "a6aedf5a-ba57-42ae-a7b1-de27edd43a12",
  "clientId": "travel-c-app-test",
  "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
  "productId": "my-product-id-123",
  "intentType": "BOOKING",
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
  "products": [
    {
      "type": "CRUISE",
      "name": "cruise name",
      "location": "Istanbul",
      "checkin": "2024-12-24",
      "checkout": "2021-12-25",
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
  "capturedAmount": 100.0,
  "authorizedAmount": 100.0,
  "refundedAmount": 50.0,
  "manualCapture": true,
  "captureDetails": [
    {
      "id": "66f2df95-659b-a21d-974d-ba3b489d50d9",
      "description": "Captured",
      "captureTime": 1727193004172,
      "amount": {
        "currency": "EUR",
        "value": 100.0
      }
    }
  ],
  "refundDetails": [
    {
      "id": "4444d000-659b-a21d-974d-ba3b489d50d9",
      "captureId": "66f2df95-659b-a21d-974d-ba3b489d50d9",
      "createTime": 1727193013453,
      "description": "Refund Description",
      "amount": {
        "currency": "EUR",
        "value": 50.0
      }
    }
  ],
  "expirationDate": 1735645380000,
  "successUrl": "https://success.com",
  "failureUrl": "https://failure.com",
  "testMode": true
}
```