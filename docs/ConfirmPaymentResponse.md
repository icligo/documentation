# ConfirmPaymentResponse

## Properties

| Name                   | Type                                                    | Description                                                                | Notes |
|------------------------|---------------------------------------------------------|----------------------------------------------------------------------------|-------|
| **date**               | **Date**                                                | The date when the event or transaction occurred.                           | -     |
| **capturedAmountInfo** | [**AmountInfo**](/documentation/dtos/#amountinfo)       | Details about the amount that had been captured.                           | -     |
| **description**        | **String**                                              | A brief description providing additional context or details if applicable. | -     |
| **captures**           | [**CaptureDetail**](/documentation/dtos/#capturedetail) | Information about individual captures related to the transaction.          | -     |


## Example

```json
{
  "date": 1727193013453,
  "capturedAmountInfo": {
    "currency": "EUR",
    "value": 10.0
  },
  "captures": [
    {
      "id": "66f2df95-659b-a21d-974d-ba3b489d50d9",
      "description": "Captured by client",
      "captureTime": 1727193004172,
      "amount": {
        "currency": "EUR",
        "value": 10.0
      }
    }
  ]
}
```
