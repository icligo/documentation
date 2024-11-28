# ClientDto

## Properties

| Name            | Type        | Description                                         | Notes      |
|-----------------|-------------|-----------------------------------------------------|------------|
| **name**        | **String**  | Name of the client.                                 | [required] |
| **email**       | **String**  | Client&#x27;s email address.                        | [optional] |
| **dateOfBirth** | **Date**    | Client&#x27;s date of birth, formatted as a string. | [optional] |
| **children**    | **Boolean** | Indicates if the client is a child.                 | [optional] |

## Example

```json
{
  "name": "Joe Doe",
  "email": "joedoe@email.com",
  "dateOfBirth": "2000-10-10",
  "children": false
}
```
