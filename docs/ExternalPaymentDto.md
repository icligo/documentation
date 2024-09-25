# ExternalPaymentDto

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **String** | Unique identifier for the payment intent. | [optional] 
**clientId** | **String** | Unique client identifier. Identifies the client that is making the request, in this case it&#x27;syour company/merchant ID agreed at the beginning of the contract. | [optional] 
**userId** | **String** | User/Customer identifier who initiated the payment. | [optional] 
**service** | **String** | Service associated with the payment. | [optional] 
**serviceDescription** | **String** | Detailed description of the service. | [optional] 
**productId** | **String** | Product identifier related to the payment. | [optional] 
**productType** | **String** | Type of the product for which the payment is being made. | [optional] 
**resume** | [**ResumeDto**](ResumeDto.md) |  | [optional] 
**products** | [**ProductDto**](ProductDto.md) | List of products associated with this payment. | [optional] 
**company** | **String** | Company associated with the payment. | [optional] 
**microsite** | **String** | Microsite used for making the payment. | [optional] 
**country** | **String** | Country where the payment is being made. | [optional] 
**currency** | **String** | Currency used for the payment. | [optional] 
**createdBy** | **String** | Username of the person who created the payment. | [optional] 
**state** | **String** | Current state of the payment. | [optional] 
**amount** | **BigDecimal** | Total amount of the order. | [optional] 
**capturedAmount** | **BigDecimal** | Amount captured. | [optional] 
**authorizedAmount** | **BigDecimal** | Amount authorized to be captured. | [optional] 
**methodTax** | **BigDecimal** | Tax applied to the payment method. | [optional] 
**captureDetails** | [**CaptureDetail**](CaptureDetail.md) | Details of the captures made for the payment. | [optional] 
**refundDetails** | [**RefundDetail**](RefundDetail.md) | Details of any refunds made for the payment. | [optional] 
**expirationDate** | **Date** | Expiration date of the payment. | [optional] 
**gifts** | [**GiftDto**](GiftDto.md) | Details of the gifts/vouchers used for the payment. | [optional] 
**isFullyPaidWithGifts** | **Boolean** | The payment is fully paid with gifts. | [optional] 

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


<a name="StateEnum"></a>
## Enum: StateEnum

* `CREATED` (value: `"CREATED"`)
* `PROCESSING` (value: `"PROCESSING"`)
* `AUTHORIZED` (value: `"AUTHORIZED"`)
* `COMPLETED` (value: `"COMPLETED"`)
* `CANCELED` (value: `"CANCELED"`)
* `FAILED` (value: `"FAILED"`)
* `REFUNDED` (value: `"REFUNDED"`)

