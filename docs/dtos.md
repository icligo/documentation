# **DTOs**

The following section defines the Data Transfer Objects (DTOs) used in our system. DTOs are simple objects designed to
carry data between processes without containing any business logic. These objects ensure efficient data exchange between
different layers or services while keeping the system modular and maintainable. Below is a list of the DTOs and their
respective fields, which are used throughout the application.

---

## [**AmountInfo**](AmountInfo.md)

**Properties**

| Name         | Type       | Description                                                                 | Notes |
|--------------|------------|-----------------------------------------------------------------------------|-------|
| **currency** | **String** | Currency code for the payment. Must respect the ISO 4217 and be upper case. | -     |
| **value**    | **Number** | The total amount of the transaction in the specified currency.              | -     |

---

## [**CancellationFeesDto**](CancellationFeesDto.md)

**Properties**

| Name          | Type       | Description                                                      | Notes      |
|---------------|------------|------------------------------------------------------------------|------------|
| **limitDate** | **Date**   | Limit date for cancellation, formatted as a string "yyyy-MM-dd". | [required] |
| **price**     | **Number** | Price of the cancellation.                                       | [required] |

---

## [**CaptureDetail**](CaptureDetail.md)

**Properties**

| Name            | Type                            | Description                                                                   | Notes |
|-----------------|---------------------------------|-------------------------------------------------------------------------------|-------|
| **id**          | **String**                      | Unique identifier for the transaction or record.                              | -     |
| **captureTime** | **long**                        | The timestamp when the transaction was captured.                              | -     |
| **description** | **String**                      | Description of the capture.                                                   | -     |
| **amount**      | [**AmountInfo**](AmountInfo.md) | Detailed information about the captured amount, including currency and value. | -     |

---

## [**CircuitDto**](CircuitDto.md)

**Properties**

| Name         | Type       | Description                                              | Notes      |
|--------------|------------|----------------------------------------------------------|------------|
| **checkin**  | **Date**   | The date and time when the check-in occurs.              | [required] |
| **checkout** | **Date**   | The date and time when the check-out occurs.             | [required] |
| **location** | **String** | The location associated with the check-in and check-out. | [optional] |

---

## [**ClientDto**](ClientDto.md)

**Properties**

| Name            | Type        | Description                                         | Notes      |
|-----------------|-------------|-----------------------------------------------------|------------|
| **name**        | **String**  | Name of the client.                                 | [required] |
| **email**       | **String**  | Client&#x27;s email address.                        | [optional] |
| **dateOfBirth** | **Date**    | Client&#x27;s date of birth, formatted as a string. | [optional] |
| **children**    | **Boolean** | Indicates if the client is a child.                 | [optional] |

---

## [**ConfirmPaymentResponse**](ConfirmPaymentResponse.md)

**Properties**

| Name                   | Type                                  | Description                                                                | Notes |
|------------------------|---------------------------------------|----------------------------------------------------------------------------|-------|
| **date**               | **Date**                              | The date when the event or transaction occurred.                           | -     |
| **capturedAmountInfo** | [**AmountInfo**](AmountInfo.md)       | Details about the amount that had been captured.                           | -     |
| **description**        | **String**                            | A brief description providing additional context or details if applicable. | -     |
| **captures**           | [**CaptureDetail**](CaptureDetail.md) | Information about individual captures related to the transaction.          | -     |

---

## [**CreateIntentRequest**](CreateIntentRequest.md)

**Properties**

| Name                        | Type                                                | Description                                                                                                                                                         | Notes      |
|-----------------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **clientId**                | **String**                                          | Unique client identifier. Identifies the client that is making the request, in this case it&#x27;syour company/merchant ID agreed at the beginning of the contract. | [required] |
| **userId**                  | **String**                                          | The user ID associated with the payment.                                                                                                                            | [required] |
| **userName**                | **String**                                          | The User name.                                                                                                                                                      | [required] |
| **userEmail**               | **String**                                          | The User e-mail.                                                                                                                                                    | [required] |
| **userContact**             | **String**                                          | The User contact.                                                                                                                                                   | [required] |
| **productId**               | **String**                                          | The ID of the product being purchased.                                                                                                                              | [required] |
| **intentType**              | [**IntentTypeEnum**](IntentTypeEnum.md)             | Type of the product.                                                                                                                                                | [required] |
| **resume**                  | [**ResumeDto**](ResumeDto.md)                       |                                                                                                                                                                     | [required] |
| **products**                | [**[ProductDto]**](ProductDto.md)                   | A list of products associated with the payment.                                                                                                                     | [required] |
| **currency**                | **String**                                          | Currency code for the payment.                                                                                                                                      | [required] |
| **company**                 | **String**                                          | Company making the payment request.                                                                                                                                 | [required] |
| **microsite**               | **String**                                          | The microsite making the payment request.                                                                                                                           | [required] |
| **country**                 | **String**                                          | Country where the payment is being made.                                                                                                                            | [required] |
| **amount**                  | **Number**                                          | The amount to be charged.                                                                                                                                           | [required] |
| **totalAmountService**      | **Number**                                          | Total amount of the service. Obs: This is NOT the value to be charged, it's for visualization purpose that covers all the service's value.                          | [required] |
| **successUrl**              | **String**                                          | The success url to redirect the user after a successful payment.                                                                                                    | [optional] |
| **failureUrl**              | **String**                                          | The failure url to redirect the user after a failure on the payment.                                                                                                | [optional] |
| **manualCapture**           | **Boolean**                                         | If the payment it will be on capture or manual form.                                                                                                                | [required] |
| **expirationDate**          | **Date**                                            | The expiration date of the intent.                                                                                                                                  | [optional] |
| **cancellationFees**        | [**[CancellationFeesDto]**](CancellationFeesDto.md) | List of cancellation fees                                                                                                                                           | [required] |
| **cancellationFeesStrings** | **String**                                          | List of cancellation fees on plain                                                                                                                                  | [required] |
| **ideaId**                  | **String**                                          | Idea identifier.                                                                                                                                                    | [required] |

---

## [**DetailDto**](DetailDto.md)

**Properties**

| Name                 | Type                                | Description                                                   | Notes      |
|----------------------|-------------------------------------|---------------------------------------------------------------|------------|
| **night**            | **Integer**                         | Number of nights for the stay.                                | [optional] |
| **roomType**         | [**RoomTypeEnum**](RoomTypeEnum.md) | Room type for accommodation.                                  | [optional] |
| **regime**           | **String**                          | Accommodation regime.                                         | [optional] |
| **flightNumber**     | **String**                          | Flight number for associated transportation.                  | [optional] |
| **departure**        | **Date**                            | Departure date for the transportation, formatted as a string. | [optional] |
| **arrival**          | **Date**                            | Arrival date for the transportation, formatted as a string.   | [optional] |
| **departureTime**    | **String**                          | Departure time for the flight or transportation.              | [optional] |
| **arrivalTime**      | **String**                          | Arrival time for the flight or transportation.                | [optional] |
| **departureAirport** | **String**                          | Departure airport code.                                       | [optional] |
| **arrivalAirport**   | **String**                          | Arrival airport code.                                         | [optional] |
| **departureCity**    | **String**                          | City of departure.                                            | [optional] |
| **arrivalCity**      | **String**                          | City of arrival.                                              | [optional] |
| **departureCountry** | **String**                          | Country of departure.                                         | [optional] |
| **arrivalCountry**   | **String**                          | Country of arrival.                                           | [optional] |
| **baggage**          | **String**                          | Baggage details for the transportation.                       | [optional] |
| **duration**         | **String**                          | Duration of the transportation or stay.                       | [optional] |
| **provider**         | **String**                          | Service provider for the product or service.                  | [optional] |
| **reception**        | **String**                          | Reception details.                                            | [optional] |
| **receptionTime**    | **Date**                            | Time of reception at the destination.                         | [optional] |
| **destinationTime**  | **Date**                            | Time of arrival at the destination.                           | [optional] |
| **destination**      | **String**                          | Destination details.                                          | [optional] |
| **circuit**          | [**CircuitDto**](CircuitDto.md)     | Details of the circuit, if applicable.                        | [optional] |
| **stopovers**        | [**StopoversDto**](StopoversDto.md) | Details of stopovers during transportation, if applicable.    | [optional] |

---

## [**ExternalCancelPaymentResponse**](ExternalCancelPaymentResponse.md)

**Properties**

| Name     | Type     | Description                | Notes |
|----------|----------|----------------------------|-------|
| **date** | **long** | Timestamp of cancellation. | -     |

---

## [**ExternalConfirmPaymentRequest**](ExternalConfirmPaymentRequest.md)

**Properties**

| Name            | Type       | Description                                                                   | Notes      |
|-----------------|------------|-------------------------------------------------------------------------------|------------|
| **amount**      | **Number** | Amount to be captured.                                                        | [required] |
| **description** | **String** | A brief description of the transaction or context for the amount information. | [optional] |

---

## [**ExternalPaymentDto**](ExternalPaymentDto.md)

**Properties**

| Name                   | Type                                     | Description                                                                                                                                | Notes |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------|
| **id**                 | **String**                               | Unique identifier for the payment intent.                                                                                                  | -     |
| **clientId**           | **String**                               | Unique client identifier.                                                                                                                  | -     |
| **userId**             | **String**                               | User/Customer identifier who initiated the payment.                                                                                        | -     |
| **service**            | **String**                               | Service associated with the payment.                                                                                                       | -     |
| **serviceDescription** | **String**                               | Detailed description of the service.                                                                                                       | -     |
| **productId**          | **String**                               | Product identifier related to the payment.                                                                                                 | -     |
| **intentType**         | [**IntentTypeEnum**](ProductTypeEnum.md) | Type of the product for which the intent is being made.                                                                                    | -     |
| **resume**             | [**ResumeDto**](ResumeDto.md)            | Resume of the service.                                                                                                                     | -     |
| **products**           | [**ProductDto**](ProductDto.md)          | List of products associated with this payment.                                                                                             | -     |
| **company**            | **String**                               | Company associated with the payment.                                                                                                       | -     |
| **microsite**          | **String**                               | Microsite used for making the payment.                                                                                                     | -     |
| **country**            | **String**                               | Country where the payment is being made.                                                                                                   | -     |
| **currency**           | **String**                               | Currency code for the payment. Must respect the ISO 4217 and be upper case.                                                                | -     |
| **createdBy**          | **String**                               | Username of the person who created the payment.                                                                                            | -     |
| **state**              | [**StateEnum**](StateEnum.md)            | Current state of the payment.                                                                                                              | -     |
| **amount**             | **Number**                               | Total amount of the order.                                                                                                                 | -     |
| **totalAmountService** | **Number**                               | Total amount of the service. Obs: This is NOT the value to be charged, it's for visualization purpose that covers all the service's value. | -     | 
| **capturedAmount**     | **Number**                               | Amount captured.                                                                                                                           | -     |
| **authorizedAmount**   | **Number**                               | Amount authorized to be captured.                                                                                                          | -     |
| **refundedAmount**     | **Number**                               | Amount refunded.                                                                                                                           | -     |
| **manualCapture**      | **Boolean**                              | If the payment is on capture or manual form.                                                                                               | -     |
| **captureDetails**     | [**CaptureDetail**](CaptureDetail.md)    | Details of the captures made for the payment.                                                                                              | -     |
| **refundDetails**      | [**RefundDetail**](RefundDetail.md)      | Details of any refunds made for the payment.                                                                                               | -     |
| **expirationDate**     | **Date**                                 | Expiration date of the payment.                                                                                                            | -     |
| **successUrl**         | **String**                               | The success url to redirect the user after a successful payment.                                                                           | -     |
| **failureUrl**         | **String**                               | The failure url to redirect the user after a failure on the payment.                                                                       | -     |
| **testMode**           | **Boolean**                              | If the payment it was created using a account.                                                                                             | -     |                                                                                                                                            |            |

---

## [**ProductDto**](ProductDto.md)

**Properties**

| Name              | Type                                      | Description                                                     | Notes                                                                        |
|-------------------|-------------------------------------------|-----------------------------------------------------------------|------------------------------------------------------------------------------|
| **type**          | [**ProductTypeEnum**](ProductTypeEnum.md) | Type of the product.                                            | [required]                                                                   |
| **name**          | **String**                                | Name of the product.                                            | [required]                                                                   |
| **location**      | **String**                                | Location of the product.                                        | [required for: ACCOMMODATION, TRANSFER, ACTIVITY, and EVENT]                 |
| **duration**      | **String**                                | Duration of the product/service.                                | [required for: ACTIVITY]                                                     |
| **code**          | **String**                                | Unique product code.                                            | [optional]                                                                   |
| **transport**     | [**TransportEnum**](TransportEnum.md)     | Type of transport associated with the product, if applicable.   | [required for: TRANSFER]                                                     |
| **checkin**       | **Date**                                  | Check-in date of the product, formatted as a string.            | [required for: FLIGHT, ACCOMMODATION, CRUISE, TRANSFER, ACTIVITY, and EVENT] |
| **checkout**      | **Date**                                  | Check-out date of the product, formatted as a string.           | [required for: ACCOMMODATION, TRANSFER, ACTIVITY, and EVENT]                 |
| **date**          | **Date**                                  | Date of the product activity or service, formatted as a string. | [optional]                                                                   |
| **price**         | **Number**                                | Price of the product.                                           | [required for: INSURANCE]                                                    |
| **detail**        | [**DetailDto**](DetailDto.md)             |                                                                 | [required for: FLIGHT, ACCOMMODATION, CRUISE, and TRANSFER]                  |
| **importantInfo** | **String**                                | String with Important information in plain text.                | [required]                                                                   |

---

## [**RefundDetail**](RefundDetail.md)

**Properties**

| Name            | Type                            | Description                                                                         | Notes |
|-----------------|---------------------------------|-------------------------------------------------------------------------------------|-------|
| **id**          | **String**                      | Unique identifier for the transaction or record.                                    | -     |
| **captureId**   | **String**                      | Identifier for the specific capture associated with the transaction. If applicable. | -     |
| **createTime**  | **long**                        | The timestamp when the refund was created.                      -                   |
| **description** | **String**                      | A brief description providing additional context about the capture.                 | -     |
| **amount**      | [**AmountInfo**](AmountInfo.md) | Detailed information about the refund.                                              | -     |

---

## [**ResumeDto**](ResumeDto.md)

**Properties**

| Name            | Type                          | Description                                                                 | Notes      |
|-----------------|-------------------------------|-----------------------------------------------------------------------------|------------|
| **description** | **String**                    | Description of the product or service.                                      | [optional] |
| **reference**   | **String**                    | Reference ID for the product or service.                                    | [optional] |
| **owner**       | **String**                    | Owner or responsible party for the transaction.                             | [required] |
| **email**       | **String**                    | Owner&#x27;s contact email address.                                         | [optional] |
| **currency**    | **String**                    | Currency code for the payment. Must respect the ISO 4217 and be upper case. | [optional] |
| **amount**      | **Number**                    | Total amount of the transaction.                                            | [optional] |
| **checkin**     | **Date**                      | Check-in date for the booking, formatted as a string.                       | [optional] |
| **checkout**    | **Date**                      | Check-out date for the booking, formatted as a string.                      | [optional] |
| **clients**     | [**ClientDto**](ClientDto.md) | List of clients involved in the transaction.                                | [optional] |

---

## [**StopoversDto**](StopoversDto.md)

**Properties**

| Name                 | Type       | Description                                                                  | Notes      |
|----------------------|------------|------------------------------------------------------------------------------|------------|
| **departure**        | **Date**   | The date and time when the departure occurs.                                 | [optional] |
| **arrival**          | **Date**   | The date and time when the arrival occurs.                                   | [optional] |
| **departureTime**    | **String** | The time of departure in a specified format (e.g., HH:MM).                   | [optional] |
| **arrivalTime**      | **String** | The time of arrival in a specified format (e.g., HH:MM).                     | [optional] |
| **departureAirport** | **String** | The airport from which the journey departs.                                  | [optional] |
| **arrivalAirport**   | **String** | The airport at which the journey arrives.                                    | [optional] |
| **departureCity**    | **String** | The city from which the journey departs.                                     | [optional] |
| **arrivalCity**      | **String** | The city at which the journey arrives.                                       | [optional] |
| **departureCountry** | **String** | The country from which the journey departs.                                  | [optional] |
| **arrivalCountry**   | **String** | The country at which the journey arrives.                                    | [optional] |
| **duration**         | **String** | The total duration of the journey, typically expressed in hours and minutes. | [optional] |

---

## [**ErrorPayloadMessage**](ErrorPayloadMessage.md)

**Properties**

| Name          | Type       | Description                                        | Notes |
|---------------|------------|----------------------------------------------------|-------|
| **timestamp** | **long**   | Timestamp of when the error occurred.              | -     |
| **status**    | **int**    | HTTP status code of the error.                     | -     |
| **error**     | **String** | HTTP description of the error.                     | -     |
| **message**   | **String** | Detailed error message.                            | -     |
| **path**      | **String** | The path of the endpoint where the error occurred. | -     |

# **Enums**

<a name="StateEnum"></a>

## [StateEnum](StateEnum.md)

* `CREATED`
* `PROCESSING`
* `AUTHORIZED`
* `COMPLETED`
* `CANCELED`
* `FAILED`
* `REFUNDED`

<a name="ProductTypeEnum"></a>

## [ProductTypeEnum](ProductTypeEnum.md)

* `ACCOMMODATION`
* `FLIGHT`
* `PACKAGE`
* `INSURANCE`
* `CRUISE`
* `ACTIVITY`
* `TRANSFER`

<a name="ProductTypeEnum"></a>

## [IntentTypeEnum](IntentTypeEnum.md)

* `BOOKING`
* `SUBSCRIPTION`
* `GIFT`
* `EVENT`
* `SERVICE`

<a name="RoomTypeEnum"></a>

## [RoomTypeEnum](RoomTypeEnum.md)

* `INSIDE`
* `OCEAN_VIEW`
* `BALCONY`
* `SUITE`

<a name="TransportEnum"></a>

## [TransportEnum](TransportEnum.md)

* `CAR`
* `BUS`
* `TRAIN` 
