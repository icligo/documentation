# AuthorizePaymentRequest

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentProvider** | **String** | The payment provider used for the transaction. |
**klarnaToken** | **String** | Token provided by Klarna for processing payments. | [optional] 
**merchantReference** | **String** | A reference code provided by the merchant to identify the transaction. | [optional] 
**country** | **String** | The country where the transaction is being processed. |
**amountInfo** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) | Detailed information about the transaction amount, including currency and total. |

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

