# RefundDetail

## Properties

| Name            | Type                            | Description                                                                         | Notes |
|-----------------|---------------------------------|-------------------------------------------------------------------------------------|-------|
| **id**          | **String**                      | Unique identifier for the transaction or record.                                    | -     |
| **captureId**   | **String**                      | Identifier for the specific capture associated with the transaction. If applicable. | -     |
| **createTime**  | **long**                        | The timestamp when the refund was created.                      -                   |
| **description** | **String**                      | A brief description providing additional context about the capture.                 | -     |
| **amount**      | [**AmountInfo**](AmountInfo.md) | Detailed information about the refund.                                              | -     |

## Example

```json
{
  "id": "4444d000-659b-a21d-974d-ba3b489d50d9",
  "captureId": "66f2df95-659b-a21d-974d-ba3b489d50d9",
  "createTime": 1727193013453,
  "description": "Refund Description",
  "amount": {
    "currency": "EUR",
    "value": 10.0
  }
}
```


