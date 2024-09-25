# AuthorizePaymentRequest

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentProvider** | **String** | The payment provider used for the transaction. |
**klarnaToken** | **String** | Token provided by Klarna for processing payments. | [optional] 
**merchantReference** | **String** | A reference code provided by the merchant to identify the transaction. | [optional] 
**country** | **String** | The country where the transaction is being processed. |
**amountInfo** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Detailed information about the transaction amount, including currency and total. |
