# AuthorizePaymentResponse

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**provider** | **String** | The service provider responsible for processing the transaction. | [optional] 
**status** | **String** | The current status of the transaction (e.g., Created, Authorized, Cancelled). | [optional] 
**_date** | **Date** | The date when the transaction took place. | [optional] 
**description** | **String** | A brief description of the transaction or its purpose. | [optional]

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

