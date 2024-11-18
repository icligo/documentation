# CreateIntentRequest

## Properties
| Name                        | Type                                                | Description                                                                                                                                                         | Notes      |
|-----------------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **clientId**                | **String**                                          | Unique client identifier. Identifies the client that is making the request, in this case it&#x27;syour company/merchant ID agreed at the beginning of the contract. | [optional] |
| **userId**                  | **String**                                          | The user ID associated with the payment.                                                                                                                            |            |
| **userName**                | **String**                                          | The User name.                                                                                                                                                      | [required] |
| **userEmail**               | **String**                                          | The User e-mail.                                                                                                                                                    | [required] |
| **userContact**             | **String**                                          | The User contact.                                                                                                                                                   | [required] |
| **productId**               | **String**                                          | The ID of the product being purchased.                                                                                                                              |            |
| **productType**             | **String**                                          | Type of the product.                                                                                                                                                |            |
| **resume**                  | [**ResumeDto**](ResumeDto.md)                       |                                                                                                                                                                     | [optional] |
| **products**                | [**[ProductDto]**](ProductDto.md)                   | A list of products associated with the payment.                                                                                                                     |            |
| **currency**                | **String**                                          | Currency code for the payment.                                                                                                                                      |            |
| **company**                 | **String**                                          | Company making the payment request.                                                                                                                                 |            |
| **microsite**               | **String**                                          | The microsite making the payment request.                                                                                                                           |            |
| **country**                 | **String**                                          | Country where the payment is being made.                                                                                                                            |            |
| **amount**                  | **Number**                                          | The amount to be charged.                                                                                                                                           |            |
| **ideaId**                  | **String**                                          | Idea identifier.                                                                                                                                                    | [required] |
| **cancellationFees**        | [**[CancellationFeesDto]**](CancellationFeesDto.md) | List of cancellation fees associated with this payment.                                                                                                             | [required] |
| **cancellationFeesStrings** | **String**                                          | List of cancellation fees on plain text                                                                                                                             | [required] |

<a name="ProductTypeEnum"></a>
## Enum: ProductTypeEnum

* `BOOKING` (value: `"BOOKING"`)
* `SUBSCRIPTION` (value: `"SUBSCRIPTION"`)
* `GIFT` (value: `"GIFT"`)
* `EVENT` (value: `"EVENT"`)
* `SERVICE` (value: `"SERVICE"`)
* `ACCOMMODATION` (value: `"ACCOMMODATION"`)
* `FLIGHT` (value: `"FLIGHT"`)
* `PACKAGE` (value: `"PACKAGE"`)
* `INSURANCE` (value: `"INSURANCE"`)
* `CRUISE` (value: `"CRUISE"`)
* `ACTIVITY` (value: `"ACTIVITY"`)
* `TRANSFER` (value: `"TRANSFER"`)

