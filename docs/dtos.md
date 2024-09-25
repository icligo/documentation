# **DTOs**
The following section defines the Data Transfer Objects (DTOs) used in our system. DTOs are simple objects designed to carry data between processes without containing any business logic. These objects ensure efficient data exchange between different layers or services while keeping the system modular and maintainable. Below is a list of the DTOs and their respective fields, which are used throughout the application.

---

## [**AmountInfo**](AmountInfo.md)

**Properties**

Name | Type | Description                                                                 | Notes
------------ | ------------- |-----------------------------------------------------------------------------| -------------
**currency** | **String** | Currency code for the payment. Must respect the ISO 4217 and be upper case. |
**value** | **Number** | The total amount of the transaction in the specified currency.              |

---
## [**AuthorizePaymentRequest**](AuthorizePaymentRequest.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**paymentProvider** | **String** | The payment provider used for the transaction. |
**klarnaToken** | **String** | Token provided by Klarna for processing payments. | [optional] 
**merchantReference** | **String** | A reference code provided by the merchant to identify the transaction. | [optional] 
**country** | **String** | The country where the transaction is being processed. |
**amountInfo** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Detailed information about the transaction amount, including currency and total. |

---
## [**AuthorizePaymentResponse**](AuthorizePaymentResponse.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**provider** | **String** | The service provider responsible for processing the transaction. | [optional] 
**status** | **String** | The current status of the transaction (e.g., Created, Authorized, Cancelled). | [optional] 
**_date** | **Date** | The date when the transaction took place. | [optional] 
**description** | **String** | A brief description of the transaction or its purpose. | [optional] 

---
## [**CaptureDetail**](CaptureDetail.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **String** | Unique identifier for the transaction or record. | [optional] 
**captureTime** | **Date** | The date and time when the transaction was captured. | [optional] 
**amount** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Detailed information about the captured amount, including currency and value. | [optional] 


---
## [**CircuitDto**](CircuitDto.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**checkin** | **Date** | The date and time when the check-in occurs. | [optional] 
**checkout** | **Date** | The date and time when the check-out occurs. | [optional] 
**location** | **String** | The location associated with the check-in and check-out. | [optional] 

---
## [**ClientDto**](ClientDto.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | **String** | Name of the client. | [optional] 
**email** | **String** | Client&#x27;s email address. | [optional] 
**dateOfBirth** | **Date** | Client&#x27;s date of birth, formatted as a string. | [optional] 
**children** | **Boolean** | Indicates if the client is a child. | [optional] 

---
## [**ConfirmPaymentResponse**](ConfirmPaymentResponse.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**status** | **String** | The current status of the process or transaction. | [optional] 
**_date** | **Date** | The date when the event or transaction occurred. | [optional] 
**capturedAmountInfo** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Details about the amount that has been captured, including currency and value. | [optional] 
**description** | **String** | A brief description providing additional context or details. | [optional] 
**captures** | [**CaptureDetail**](/documentation/dtos/#capturedetail) | Information about individual captures related to the transaction. | [optional] 

---
## [**DetailDto**](DetailDto.md)

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
**circuit** | [**CircuitDto**](/documentation/dtos/#circuitdto) | Details of the circuit, if applicable. | [optional] 
**stopovers** | [**StopoversDto**](/documentation/dtos/#stopoversdto) | Details of stopovers during transportation, if applicable. | [optional] 

<a name="RoomTypeEnum"></a>
**Enum: RoomTypeEnum**

* `inside` (value: `"Inside"`)
* `oceanview` (value: `"Oceanview"`)
* `balcony` (value: `"Balcony"`)
* `suite` (value: `"Suite"`)

---
## [**ErrorPayloadMessage**](ErrorPayloadMessage.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**timestamp** | **Number** | Timestamp of when the error occurred. | [optional] 
**status** | **Number** | HTTP status code of the error. | [optional] 
**error** | **String** | HTTP description of the error. | [optional] 
**message** | **String** | Detailed error message. | [optional] 
**path** | **String** | The path of the endpoint where the error occurred. | [optional] 

---

## [**ExternalCancelPaymentResponse**](ExternalCancelPaymentResponse.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**date** | **Date** | Time of cancel payment intent. |

---
## [**ExternalConfirmPaymentRequest**](ExternalConfirmPaymentRequest.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**amountInfo** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Detailed information about the captured amount, including currency and value. |
**description** | **String** | A brief description of the transaction or context for the amount information. | [optional] 


---

## [**ExternalPaymentDto**](ExternalPaymentDto.md)

**Properties**

Name | Type | Description                                                                 | Notes
------------ | ------------- |-----------------------------------------------------------------------------| -------------
**id** | **String** | Unique identifier for the payment intent.                                   | [optional] 
**clientId** | **String** | Unique client identifier.                                                   | [optional] 
**userId** | **String** | User/Customer identifier who initiated the payment.                         | [optional] 
**service** | **String** | Service associated with the payment.                                        | [optional] 
**serviceDescription** | **String** | Detailed description of the service.                                        | [optional] 
**productId** | **String** | Product identifier related to the payment.                                  | [optional] 
**productType** | **String** | Type of the product for which the payment is being made.                    | [optional] 
**resume** | [**ResumeDto**](/documentation/dtos/#resumedto) |                                                                             | [optional] 
**products** | [**ProductDto**](/documentation/dtos/#productdto) | List of products associated with this payment.                              | [optional] 
**company** | **String** | Company associated with the payment.                                        | [optional] 
**microsite** | **String** | Microsite used for making the payment.                                      | [optional] 
**country** | **String** | Country where the payment is being made.                                    | [optional] 
**currency** | **String** | Currency code for the payment. Must respect the ISO 4217 and be upper case. | [optional] 
**createdBy** | **String** | Username of the person who created the payment.                             | [optional] 
**state** | **String** | Current state of the payment.                                               | [optional] 
**amount** | **Number** | Total amount of the order.                                                  | [optional] 
**capturedAmount** | **Number** | Amount captured.                                                            | [optional] 
**authorizedAmount** | **Number** | Amount authorized to be captured.                                           | [optional] 
**methodTax** | **Number** | Tax applied to the payment method.                                          | [optional] 
**captureDetails** | [**CaptureDetail**](/documentation/dtos/#capturedetail) | Details of the captures made for the payment.                               | [optional] 
**refundDetails** | [**RefundDetail**](/documentation/dtos/#refunddetail) | Details of any refunds made for the payment.                                | [optional] 
**expirationDate** | **Date** | Expiration date of the payment.                                             | [optional] 
**gifts** | [**GiftDto**](/documentation/dtos/#giftdto) | Details of the gifts/vouchers used for the payment.                         | [optional] 
**isFullyPaidWithGifts** | **Boolean** | The payment is fully paid with gifts.                                       | [optional] 

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
## [**GiftDto**](GiftDto.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **Number** | Unique identifier for the record or entity. | [optional] 
**value** | **Number** | The total amount associated with the transaction or record. | [optional] 
**valueToUse** | **Number** | The amount that should be utilized for processing or calculations. | [optional] 
**code** | **String** | A reference code related to the transaction or entity. | [optional] 
**clientName** | **String** | The name of the client associated with the transaction. | [optional] 
**refund** | **Boolean** | Indicates whether the transaction involves a refund (true) or not (false). | [optional] 
**fkType** | **Number** | Foreign key reference to another entity or type. | [optional] 

---
## [**ProductDto**](ProductDto.md)

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
**detail** | [**DetailDto**](/documentation/dtos/#detaildto) |  | [optional] 

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
## [**RefundDetail**](RefundDetail.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | **String** | Unique identifier for the transaction or record. | [optional] 
**captureId** | **String** | Identifier for the specific capture associated with the transaction. | [optional] 
**createTime** | **Date** | The date and time when the capture was created. | [optional] 
**description** | **String** | A brief description providing additional context about the capture. | [optional] 
**amount** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Detailed information about the capture amount, including currency and value. | [optional] 

---
## [**RefundEndpointPaymentRequest**](RefundEndpointPaymentRequest.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**amountInfo** | [**AmountInfo**](/documentation/dtos/#amountinfo) | Detailed information about the amount involved in the transaction, including currency and value. |
**description** | **String** | A brief description providing additional context or details about the refund. | [optional] 


---

## [**ResumeDto**](ResumeDto.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**description** | **String** | Description of the product or service. | [optional] 
**reference** | **String** | Reference ID for the product or service. | [optional] 
**owner** | **String** | Owner or responsible party for the transaction. | [optional] 
**email** | **String** | Owner&#x27;s contact email address. | [optional] 
**currency** | **String** | Currency code for the payment. Must respect the ISO 4217 and be upper case. | [optional] 
**amount** | **Number** | Total amount of the transaction. | [optional] 
**checkin** | **Date** | Check-in date for the booking, formatted as a string. | [optional] 
**checkout** | **Date** | Check-out date for the booking, formatted as a string. | [optional] 
**clients** | [**ClientDto**](/documentation/dtos/#clientdto) | List of clients involved in the transaction. | [optional] 

---
## [**StopoversDto**](StopoversDto.md)

**Properties**

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**departure** | **Date** | The date and time when the departure occurs. | [optional] 
**arrival** | **Date** | The date and time when the arrival occurs. | [optional] 
**departureTime** | **String** | The time of departure in a specified format (e.g., HH:MM). | [optional] 
**arrivalTime** | **String** | The time of arrival in a specified format (e.g., HH:MM). | [optional] 
**departureAirport** | **String** | The airport from which the journey departs. | [optional] 
**arrivalAirport** | **String** | The airport at which the journey arrives. | [optional] 
**departureCity** | **String** | The city from which the journey departs. | [optional] 
**arrivalCity** | **String** | The city at which the journey arrives. | [optional] 
**departureCountry** | **String** | The country from which the journey departs. | [optional] 
**arrivalCountry** | **String** | The country at which the journey arrives. | [optional] 
**duration** | **String** | The total duration of the journey, typically expressed in hours and minutes. | [optional] 
