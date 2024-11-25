# ExternalPaymentDto

## Properties

| Name                   | Type                          | Description                                                                                                                                | Notes |
|------------------------|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------|
| **id**                 | **String**                    | Unique identifier for the payment intent.                                                                                                  |       |
| **clientId**           | **String**                    | Unique client identifier.                                                                                                                  |       |
| **userId**             | **String**                    | User/Customer identifier who initiated the payment.                                                                                        |       |
| **service**            | **String**                    | Service associated with the payment.                                                                                                       |       |
| **serviceDescription** | **String**                    | Detailed description of the service.                                                                                                       |       |
| **productId**          | **String**                    | Product identifier related to the payment.                                                                                                 |       |
| **productType**        | [**ProductTypeEnum**](ProductTypeEnum.md)                        | Type of the product for which the payment is being made.                                                                                   |       |
| **resume**             | [**ResumeDto**](ResumeDto.md) | Resume of the service.                                                                                                                     |       |
| **products**           | [**ProductDto**](ProductDto.md) | List of products associated with this payment.                                                                                             |       |
| **company**            | **String**                    | Company associated with the payment.                                                                                                       |       |
| **microsite**          | **String**                    | Microsite used for making the payment.                                                                                                     |       |
| **country**            | **String**                    | Country where the payment is being made.                                                                                                   |       |
| **currency**           | **String**                    | Currency code for the payment. Must respect the ISO 4217 and be upper case.                                                                |       |
| **createdBy**          | **String**                    | Username of the person who created the payment.                                                                                            |       |
| **state**              | [**StateEnum**](StateEnum.md)                        | Current state of the payment.                                                                                                              |       |
| **amount**             | **BigDecimal**                | Total amount of the order.                                                                                                                 |       |
| **totalAmountService** | **Number**                    | Total amount of the service. Obs: This is NOT the value to be charged, it's for visualization purpose that covers all the service's value. |       | 
| **capturedAmount**     | **BigDecimal**                | Amount captured.                                                                                                                           |       |
| **authorizedAmount**   | **BigDecimal**                | Amount authorized to be captured.                                                                                                          |       |
| **refundedAmount**     | **BigDecimal**                | Amount refunded.                                                                                                                           |       |
| **manualCapture**      | **Boolean**                   | If the payment is on capture or manual form.                                                                                               |       |
| **captureDetails**     | [**CaptureDetail**](CaptureDetail.md) | Details of the captures made for the payment.                                                                                              |       |
| **refundDetails**      | [**RefundDetail**](RefundDetail.md) | Details of any refunds made for the payment.                                                                                               |       |
| **expirationDate**     | **Date**                      | Expiration date of the payment.                                                                                                            |       |
| **successUrl**         | **String**                    | The success url to redirect the user after a successful payment.                                                                           |       |
| **failureUrl**         | **String**                    | The failure url to redirect the user after a failure on the payment.                                                                       |       |
| **testMode**           | **Boolean**                   | If the payment it was created using a account.                                                                                             |       |                                                                                                                                            |            |