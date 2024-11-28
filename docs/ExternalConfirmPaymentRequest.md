# ExternalConfirmPaymentRequest

## Properties

| Name            | Type       | Description                                                                   | Notes      |
|-----------------|------------|-------------------------------------------------------------------------------|------------|
| **amount**      | **Number** | Amount to be captured.                                                        | [required] |
| **description** | **String** | A brief description of the transaction or context for the amount information. | [optional] |

## Example

```json
{
    "amount": 100,
    "description": "Captured by client"
}
```
