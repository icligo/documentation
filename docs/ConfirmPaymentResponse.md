# ConfirmPaymentResponse

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**status** | **String** | The current status of the process or transaction. | [optional] 
**_date** | **Date** | The date when the event or transaction occurred. | [optional] 
**capturedAmountInfo** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) | Details about the amount that has been captured, including currency and value. | [optional] 
**description** | **String** | A brief description providing additional context or details. | [optional] 
**captures** | [**CaptureDetail**](/mkdocs/dtos/#capturedetail) | Information about individual captures related to the transaction. | [optional] 
