# CancellationFeesDto

## Properties

| Name          | Type       | Description                                                                    | Notes      |
|---------------|------------|--------------------------------------------------------------------------------|------------|
| **limitDate** | **Date**   | Limit date for cancellation, formatted as a string "yyyy-MM-dd".               | [required] |
| **price**     | **Number** | Price of the cancellation. Currency it is associated to the intent's currency. | [required] |

## Example

```json
{
  "limitDate": "2000-12-12",
  "price": 10
}
```
