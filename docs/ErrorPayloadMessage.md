# ErrorPayloadMessage

## Properties

| Name          | Type       | Description                                        | Notes |
|---------------|------------|----------------------------------------------------|-------|
| **timestamp** | **long**   | Timestamp of when the error occurred.              | -     |
| **status**    | **int**    | HTTP status code of the error.                     | -     |
| **error**     | **String** | HTTP description of the error.                     | -     |
| **message**   | **String** | Detailed error message.                            | -     |
| **path**      | **String** | The path of the endpoint where the error occurred. | -     |

## Example

```json
{
  "timestamp": 1732724287772,
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid request payload. Reason(s): {'example[0].example':'Cannot be null'}",
  "path": "/payments/create-payment-intent"
}
```