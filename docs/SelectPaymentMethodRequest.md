# SelectPaymentMethodRequest

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentMethod** | **String** | The method used for payment. |
**provider** | **String** | The service provider facilitating the payment (e.g., Stripe, PayPal). |
**mbWayNumber** | **String** | The mobile number associated with the MB Way payment method. | [optional] 
**stripeMethodId** | **String** | Unique identifier for the payment method in Stripe's system. | [optional]

<a name="PaymentMethodEnum"></a>
## Enum: PaymentMethodEnum

* `VISA` (value: `"VISA"`)
* `PAYPAL` (value: `"PAYPAL"`)
* `MASTERCARD` (value: `"MASTERCARD"`)
* `AMERICANEXPRESS` (value: `"AMERICANEXPRESS"`)
* `MULTIBANCO` (value: `"MULTIBANCO"`)
* `MBWAY` (value: `"MBWAY"`)
* `KLARNA` (value: `"KLARNA"`)
* `ICLIGOGIFT` (value: `"ICLIGOGIFT"`)


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

