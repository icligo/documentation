# PaymentExceptionPayload

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**translationKey** | **String** | Key used for translating the error message. | [optional] 
**message** | **String** | Detailed error message related to the payment exception. | [optional] 
**action** | **String** | Action to be taken based on the payment exception. | [optional] 

<a name="TranslationKeyEnum"></a>
## Enum: TranslationKeyEnum

* `PAYMENT_API_ERROR_NAME` (value: `"PAYMENT_API_ERROR_NAME"`)
* `PAYMENT_API_ERROR_FIELD` (value: `"PAYMENT_API_ERROR_FIELD"`)
* `PAYMENT_API_ERROR_CREATING_ORDER` (value: `"PAYMENT_API_ERROR_CREATING_ORDER"`)
* `PAYMENT_API_ERROR_STATE` (value: `"PAYMENT_API_ERROR_STATE"`)
* `GIFT_API_ERROR` (value: `"GIFT_API_ERROR"`)
* `PAYMENT_API_ERROR_CAPTURE` (value: `"PAYMENT_API_ERROR_CAPTURE"`)
* `PAYMENT_API_ERROR_CANCELLATION` (value: `"PAYMENT_API_ERROR_CANCELLATION"`)
* `PAYMENT_API_ERROR_REFUND` (value: `"PAYMENT_API_ERROR_REFUND"`)
* `PAYMENT_API_ID_NOT_FOUND` (value: `"PAYMENT_API_ID_NOT_FOUND"`)
* `PAYMENT_API_INVALID_SELECTED_METHOD` (value: `"PAYMENT_API_INVALID_SELECTED_METHOD"`)
* `PAYMENT_API_ALREADY_CANCELLED` (value: `"PAYMENT_API_ALREADY_CANCELLED"`)
* `PAYMENT_API_TIMEOUT` (value: `"PAYMENT_API_TIMEOUT"`)


<a name="ActionEnum"></a>
## Enum: ActionEnum

* `INFO` (value: `"INFO"`)
* `WARNING` (value: `"WARNING"`)
* `CLOSE` (value: `"CLOSE"`)

