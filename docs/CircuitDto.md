# CircuitDto

## Properties

| Name         | Type       | Description                                              | Notes      |
|--------------|------------|----------------------------------------------------------|------------|
| **checkin**  | **Date**   | The date and time when the check-in occurs.              | [required] |
| **checkout** | **Date**   | The date and time when the check-out occurs.             | [required] |
| **location** | **String** | The location associated with the check-in and check-out. | [optional] |

## Example

```json
{
  "checkin": "2024-12-24T11:03:42.501+00:00",
  "checkout": "2024-12-24T11:03:42.501+00:00",
  "location": "Turkey"
}
```
