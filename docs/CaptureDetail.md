# CaptureDetail

## Properties

| Name            | Type                            | Description                                                                   | Notes |
|-----------------|---------------------------------|-------------------------------------------------------------------------------|-------|
| **id**          | **String**                      | Unique identifier for the transaction or record.                              | -     |
| **captureTime** | **long**                        | The timestamp when the transaction was captured.                              | -     |
| **description** | **String**                      | Description of the capture.                                                   | -     |
| **amount**      | [**AmountInfo**](AmountInfo.md) | Detailed information about the captured amount, including currency and value. | -     |

## Example

```json
{
  "id": "66f2df95-659b-a21d-974d-ba3b489d50d9",
  "description": "Captured by client",
  "captureTime": 1727193004172,
  "amount": {
    "currency": "EUR",
    "value": 10
  }
}
```

