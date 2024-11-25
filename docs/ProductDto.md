## Properties
| Name              | Type                                      | Description                                                     | Notes      |
|-------------------|-------------------------------------------|-----------------------------------------------------------------|------------|
| **type**          | [**ProductTypeEnum**](ProductTypeEnum.md) | Type of the product.                                            | [optional] |
| **name**          | **String**                                | Name of the product.                                            | [required] |
| **location**      | **String**                                | Location of the product.                                        | [optional] |
| **duration**      | **String**                                | Duration of the product/service.                                | [optional] |
| **code**          | **String**                                | Unique product code.                                            | [optional] |
| **transport**     | [**TransportEnum**](ProductTypeEnum.md)   | Type of transport associated with the product, if applicable.   | [optional] |
| **checkin**       | **Date**                                  | Check-in date of the product, formatted as a string.            | [optional] |
| **checkout**      | **Date**                                  | Check-out date of the product, formatted as a string.           | [optional] |
| **_date**         | **Date**                                  | Date of the product activity or service, formatted as a string. | [optional] |
| **price**         | **Number**                                | Price of the product.                                           | [optional] |
| **detail**        | [**DetailDto**](DetailDto.md)             |                                                                 | [optional] |
| **importantInfo** | **String**                                | String with Important information in plain text.                | [required] |

