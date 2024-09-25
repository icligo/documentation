# CreatePaymentResponse

## Properties
Name | Type           | Description                                                                 | Notes
------------ |----------------|-----------------------------------------------------------------------------| -------------
**createdPaymentId** | **String**     |                                                                             | [optional] 
**provider** | **String**     |                                                                             | [optional] 
**require3DSecure** | **Boolean**    |                                                                             | [optional] 
**status** | **String**     |                                                                             | [optional] 
**createdAt** | **Date**       |                                                                             | [optional] 
**reference** | **String**     |                                                                             | [optional] 
**entity** | **String**     |                                                                             | [optional] 
**clientSecret** | **String**     |                                                                             | [optional] 
**clientToken** | **String**     |                                                                             | [optional] 
**amount** | **Double** |                                                                             | [optional] 
**currency** | **String**     | Currency code for the payment. Must respect the ISO 4217 and be upper case. | [optional] 
**redirectUrl** | **String**     |                                                                             | [optional] 

<a name="ProviderEnum"></a>
## Enum: ProviderEnum

* `STRIPE_PT` (value: `"STRIPE_PT"`)
* `VIVAWALLET_PT` (value: `"VIVAWALLET_PT"`)
* `IFTHEN_PT` (value: `"IFTHEN_PT"`)
* `PAYPAL_PT` (value: `"PAYPAL_PT"`)
* `PAYPAL_US` (value: `"PAYPAL_US"`)
* `REVOLUT_PT` (value: `"REVOLUT_PT"`)
* `KLARNA_PT` (value: `"KLARNA_PT"`)
* `ICLIGO` (value: `"ICLIGO"`)

