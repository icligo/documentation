# AuthorizePaymentRequest

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentProvider** | **String** |  | 
**klarnaToken** | **String** |  | [optional] 
**merchantReference** | **String** |  | [optional] 
**country** | **String** |  | 
**amountInfo** | [**AmountInfo**](AmountInfo.md) |  | 

<a name="PaymentProviderEnum"></a>
## Enum: PaymentProviderEnum

* `STRIPE_PT` (value: `"STRIPE_PT"`)
* `VIVAWALLET_PT` (value: `"VIVAWALLET_PT"`)
* `IFTHEN_PT` (value: `"IFTHEN_PT"`)
* `PAYPAL_PT` (value: `"PAYPAL_PT"`)
* `PAYPAL_US` (value: `"PAYPAL_US"`)
* `REVOLUT_PT` (value: `"REVOLUT_PT"`)
* `KLARNA_PT` (value: `"KLARNA_PT"`)
* `ICLIGO` (value: `"ICLIGO"`)

