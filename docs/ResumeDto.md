# ResumeDto

## Properties

| Name            | Type                          | Description                                                                 | Notes      |
|-----------------|-------------------------------|-----------------------------------------------------------------------------|------------|
| **description** | **String**                    | Description of the product or service.                                      | [optional] |
| **reference**   | **String**                    | Reference ID for the product or service.                                    | [optional] |
| **owner**       | **String**                    | Owner or responsible party for the transaction.                             | [required] |
| **email**       | **String**                    | Owner&#x27;s contact email address.                                         | [optional] |
| **currency**    | **String**                    | Currency code for the payment. Must respect the ISO 4217 and be upper case. | [optional] |
| **amount**      | **Number**                    | Total amount of the transaction.                                            | [optional] |
| **checkin**     | **Date**                      | Check-in date for the booking, formatted as a string.                       | [optional] |
| **checkout**    | **Date**                      | Check-out date for the booking, formatted as a string.                      | [optional] |
| **clients**     | [**ClientDto**](ClientDto.md) | List of clients involved in the transaction.                                | [optional] |

## Example

```json
{
  "owner": "Bob Smith",
  "reference": "REF901",
  "email": "bobsmith@email.com",
  "currency": "EUR",
  "amount": 10,
  "checkin": "2024-09-24T16:46:42.411Z",
  "checkout": "2024-09-24T16:46:42.411Z",
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
}
```
