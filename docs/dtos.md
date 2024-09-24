# **DTOs**
The following section defines the Data Transfer Objects (DTOs) used in our system. DTOs are simple objects designed to carry data between processes without containing any business logic. These objects ensure efficient data exchange between different layers or services while keeping the system modular and maintainable. Below is a list of the DTOs and their respective fields, which are used throughout the application.

---

## **AmountInfo**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**currency** | **String** |  | 
**value** | **Number** |  | 

---
## **AuthorizePaymentRequest**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentProvider** | **String** |  | 
**klarnaToken** | **String** |  | [optional] 
**merchantReference** | **String** |  | [optional] 
**country** | **String** |  | 
**amountInfo** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) |  | 

<a name="PaymentProviderEnum"></a>
**Enum: PaymentProviderEnum**

* `STRIPE_PT` (value: `"STRIPE_PT"`)
* `VIVAWALLET_PT` (value: `"VIVAWALLET_PT"`)
* `IFTHEN_PT` (value: `"IFTHEN_PT"`)
* `PAYPAL_PT` (value: `"PAYPAL_PT"`)
* `PAYPAL_US` (value: `"PAYPAL_US"`)
* `REVOLUT_PT` (value: `"REVOLUT_PT"`)
* `KLARNA_PT` (value: `"KLARNA_PT"`)
* `ICLIGO` (value: `"ICLIGO"`)

---
## **AuthorizePaymentResponse**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**provider** | **String** |  | [optional] 
**status** | **String** |  | [optional] 
**_date** | **Date** |  | [optional] 
**description** | **String** |  | [optional] 

<a name="ProviderEnum"></a>
**Enum: ProviderEnum**

* `STRIPE_PT` (value: `"STRIPE_PT"`)
* `VIVAWALLET_PT` (value: `"VIVAWALLET_PT"`)
* `IFTHEN_PT` (value: `"IFTHEN_PT"`)
* `PAYPAL_PT` (value: `"PAYPAL_PT"`)
* `PAYPAL_US` (value: `"PAYPAL_US"`)
* `REVOLUT_PT` (value: `"REVOLUT_PT"`)
* `KLARNA_PT` (value: `"KLARNA_PT"`)
* `ICLIGO` (value: `"ICLIGO"`)

---
## **CaptureDetail**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **String** |  | [optional] 
**captureTime** | **Date** |  | [optional] 
**amount** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) |  | [optional] 

---
## **CircuitDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**checkin** | **Date** |  | [optional] 
**checkout** | **Date** |  | [optional] 
**location** | **String** |  | [optional] 

---
## **ClientDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | **String** | Name of the client. | [optional] 
**email** | **String** | Client&#x27;s email address. | [optional] 
**dateOfBirth** | **Date** | Client&#x27;s date of birth, formatted as a string. | [optional] 
**children** | **Boolean** | Indicates if the client is a child. | [optional] 

---
## **ConfirmPaymentResponse**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**status** | **String** |  | [optional] 
**_date** | **Date** |  | [optional] 
**capturedAmountInfo** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) |  | [optional] 
**description** | **String** |  | [optional] 
**captures** | [**CaptureDetail**](/mkdocs/dtos/#capturedetail) |  | [optional] 

---
## **DetailDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**night** | **Number** | Number of nights for the stay. | [optional] 
**roomType** | **String** | Room type for accommodation. | [optional] 
**regime** | **String** | Accommodation regime. | [optional] 
**flightNumber** | **String** | Flight number for associated transportation. | [optional] 
**departure** | **Date** | Departure date for the transportation, formatted as a string. | [optional] 
**arrival** | **Date** | Arrival date for the transportation, formatted as a string. | [optional] 
**departureTime** | **String** | Departure time for the flight or transportation. | [optional] 
**arrivalTime** | **String** | Arrival time for the flight or transportation. | [optional] 
**departureAirport** | **String** | Departure airport code. | [optional] 
**arrivalAirport** | **String** | Arrival airport code. | [optional] 
**departureCity** | **String** | City of departure. | [optional] 
**arrivalCity** | **String** | City of arrival. | [optional] 
**departureCountry** | **String** | Country of departure. | [optional] 
**arrivalCountry** | **String** | Country of arrival. | [optional] 
**baggage** | **String** | Baggage details for the transportation. | [optional] 
**duration** | **String** | Duration of the transportation or stay. | [optional] 
**provider** | **String** | Service provider for the product or service. | [optional] 
**reception** | **String** | Reception details. | [optional] 
**receptionTime** | **Date** | Time of reception at the destination. | [optional] 
**destinationTime** | **Date** | Time of arrival at the destination. | [optional] 
**destination** | **String** | Destination details. | [optional] 
**circuit** | [**CircuitDto**](/mkdocs/dtos/#circuitdto) | Details of the circuit, if applicable. | [optional] 
**stopovers** | [**StopoversDto**](/mkdocs/dtos/#stopoversdto) | Details of stopovers during transportation, if applicable. | [optional] 

<a name="RoomTypeEnum"></a>
**Enum: RoomTypeEnum**

* `inside` (value: `"Inside"`)
* `oceanview` (value: `"Oceanview"`)
* `balcony` (value: `"Balcony"`)
* `suite` (value: `"Suite"`)

---
## **ErrorPayloadMessage**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**timestamp** | **Number** | Timestamp of when the error occurred. | [optional] 
**status** | **Number** | HTTP status code of the error. | [optional] 
**error** | **String** | HTTP description of the error. | [optional] 
**message** | **String** | Detailed error message. | [optional] 
**path** | **String** | The path of the endpoint where the error occurred. | [optional] 
**metadata** | [**PaymentExceptionPayload**](/mkdocs/dtos/#paymentexceptionpayload) |  | [optional] 

---
## **ExternalConfirmPaymentRequest**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**amountInfo** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) |  | 
**description** | **String** |  | [optional] 

---
## **GiftDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **Number** |  | [optional] 
**value** | **Number** |  | [optional] 
**valueToUse** | **Number** |  | [optional] 
**code** | **String** |  | [optional] 
**clientName** | **String** |  | [optional] 
**refund** | **Boolean** |  | [optional] 
**fkType** | **Number** |  | [optional] 

---
## **PaymentDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **String** | Unique identifier for the payment intent. | [optional] 
**clientId** | **String** | Unique client identifier. Identifies the client that is making the request, in this case it&#x27;syour company/merchant ID agreed at the beginning of the contract. | [optional] 
**userId** | **String** | User/Customer identifier who initiated the payment. | [optional] 
**service** | **String** | Service associated with the payment. | [optional] 
**serviceDescription** | **String** | Detailed description of the service. | [optional] 
**productId** | **String** | Product identifier related to the payment. | [optional] 
**productType** | **String** | Type of the product for which the payment is being made. | [optional] 
**resume** | [**ResumeDto**](/mkdocs/dtos/#resumedto) |  | [optional] 
**products** | [**ProductDto**](/mkdocs/dtos/#productdto) | List of products associated with this payment. | [optional] 
**company** | **String** | Company associated with the payment. | [optional] 
**microsite** | **String** | Microsite used for making the payment. | [optional] 
**country** | **String** | Country where the payment is being made. | [optional] 
**currency** | **String** | Currency used for the payment. | [optional] 
**createdBy** | **String** | Username of the person who created the payment. | [optional] 
**state** | **String** | Current state of the payment. | [optional] 
**amount** | **Number** | Total amount of the order. | [optional] 
**capturedAmount** | **Number** | Amount captured. | [optional] 
**authorizedAmount** | **Number** | Amount authorized to be captured. | [optional] 
**methodTax** | **Number** | Tax applied to the payment method. | [optional] 
**captureDetails** | [**CaptureDetail**](/mkdocs/dtos/#capturedetail) | Details of the captures made for the payment. | [optional] 
**refundDetails** | [**RefundDetail**](/mkdocs/dtos/#refunddetail) | Details of any refunds made for the payment. | [optional] 
**expirationDate** | **Date** | Expiration date of the payment. | [optional] 
**gifts** | [**GiftDto**](/mkdocs/dtos/#giftdto) | Details of the gifts/vouchers used for the payment. | [optional] 
**isFullyPaidWithGifts** | **Boolean** | The payment is fully paid with gifts. | [optional] 

<a name="ProductTypeEnum"></a>
**Enum: ProductTypeEnum**

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
**Enum: StateEnum**

* `CREATED` (value: `"CREATED"`)
* `PROCESSING` (value: `"PROCESSING"`)
* `AUTHORIZED` (value: `"AUTHORIZED"`)
* `COMPLETED` (value: `"COMPLETED"`)
* `CANCELED` (value: `"CANCELED"`)
* `FAILED` (value: `"FAILED"`)
* `REFUNDED` (value: `"REFUNDED"`)

---
## **PaymentExceptionPayload**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**translationKey** | **String** | Key used for translating the error message. | [optional] 
**message** | **String** | Detailed error message related to the payment exception. | [optional] 
**action** | **String** | Action to be taken based on the payment exception. | [optional] 

<a name="TranslationKeyEnum"></a>
**Enum: TranslationKeyEnum**

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
**Enum: ActionEnum**

* `INFO` (value: `"INFO"`)
* `WARNING` (value: `"WARNING"`)
* `CLOSE` (value: `"CLOSE"`)

---
## **ProductDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**type** | **String** | Type of the product. | [optional] 
**name** | **String** | Name of the product. | [optional] 
**location** | **String** | Location of the product. | [optional] 
**duration** | **String** | Duration of the product/service. | [optional] 
**code** | **String** | Unique product code. | [optional] 
**transport** | **String** | Type of transport associated with the product, if applicable. | [optional] 
**checkin** | **Date** | Check-in date of the product, formatted as a string. | [optional] 
**checkout** | **Date** | Check-out date of the product, formatted as a string. | [optional] 
**_date** | **Date** | Date of the product activity or service, formatted as a string. | [optional] 
**price** | **Number** | Price of the product. | [optional] 
**detail** | [**DetailDto**](/mkdocs/dtos/#detaildto) |  | [optional] 

<a name="TypeEnum"></a>
**Enum: TypeEnum**

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


<a name="TransportEnum"></a>
**Enum: TransportEnum**

* `CAR` (value: `"CAR"`)
* `BUS` (value: `"BUS"`)
* `TRAIN` (value: `"TRAIN"`)

---
## **RefundDetail**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **String** |  | [optional] 
**captureId** | **String** |  | [optional] 
**createTime** | **Date** |  | [optional] 
**description** | **String** |  | [optional] 
**amount** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) |  | [optional] 

---
## **RefundEndpointPaymentRequest**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**amountInfo** | [**AmountInfo**](/mkdocs/dtos/#amountinfo) |  | 
**description** | **String** |  | [optional] 

---

## **ResumeDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**description** | **String** | Description of the product or service. | [optional] 
**reference** | **String** | Reference ID for the product or service. | [optional] 
**owner** | **String** | Owner or responsible party for the transaction. | [optional] 
**email** | **String** | Owner&#x27;s contact email address. | [optional] 
**currency** | **String** | Currency code for the transaction. | [optional] 
**amount** | **Number** | Total amount of the transaction. | [optional] 
**checkin** | **Date** | Check-in date for the booking, formatted as a string. | [optional] 
**checkout** | **Date** | Check-out date for the booking, formatted as a string. | [optional] 
**clients** | [**ClientDto**](/mkdocs/dtos/#clientdto) | List of clients involved in the transaction. | [optional] 

---

## **SelectPaymentMethodRequest**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentMethod** | **String** |  | 
**provider** | **String** |  | 
**mbWayNumber** | **String** |  | [optional] 
**stripeMethodId** | **String** |  | [optional] 

<a name="PaymentMethodEnum"></a>
**Enum: PaymentMethodEnum**

* `VISA` (value: `"VISA"`)
* `PAYPAL` (value: `"PAYPAL"`)
* `MASTERCARD` (value: `"MASTERCARD"`)
* `AMERICANEXPRESS` (value: `"AMERICANEXPRESS"`)
* `MULTIBANCO` (value: `"MULTIBANCO"`)
* `MBWAY` (value: `"MBWAY"`)
* `KLARNA` (value: `"KLARNA"`)
* `ICLIGOGIFT` (value: `"ICLIGOGIFT"`)


<a name="ProviderEnum"></a>
**Enum: ProviderEnum**

* `STRIPE_PT` (value: `"STRIPE_PT"`)
* `VIVAWALLET_PT` (value: `"VIVAWALLET_PT"`)
* `IFTHEN_PT` (value: `"IFTHEN_PT"`)
* `PAYPAL_PT` (value: `"PAYPAL_PT"`)
* `PAYPAL_US` (value: `"PAYPAL_US"`)
* `REVOLUT_PT` (value: `"REVOLUT_PT"`)
* `KLARNA_PT` (value: `"KLARNA_PT"`)
* `ICLIGO` (value: `"ICLIGO"`)

---

## **StopoversDto**

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**departure** | **Date** |  | [optional] 
**arrival** | **Date** |  | [optional] 
**departureTime** | **String** |  | [optional] 
**arrivalTime** | **String** |  | [optional] 
**departureAirport** | **String** |  | [optional] 
**arrivalAirport** | **String** |  | [optional] 
**departureCity** | **String** |  | [optional] 
**arrivalCity** | **String** |  | [optional] 
**departureCountry** | **String** |  | [optional] 
**arrivalCountry** | **String** |  | [optional] 
**duration** | **String** |  | [optional] 