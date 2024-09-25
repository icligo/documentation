# **iCliGo Payment API Documentation**

This API allows you to manage payment intents, enabling payment capture, cancellations, and refunds.

---

## **Authentication**

To authenticate, include the following headers with all your API requests:

- **X-Application-Id**: Your application ID.
- **X-Access-Token**: A token used to authenticate your application's access to the API.

The API will return a **400 Bad Request** response if these headers are missing or invalid. If the payment request is associated with an unauthorized or incorrect Application ID, a **401 Unauthorised** response will be returned. If an attempt is made to access a forbidden resource, a **403 Forbidden** response is returned.


## **Errors**
We have normalized the error payload, where all the errors obey the same format in order to be easier to read the error.

The error payload includes the following parameters:

| Parameter | Type   | Description                                                       | Example                                     |
| --------- | ------ | ----------------------------------------------------------------- | ------------------------------------------- |
| timestamp | long   | Unix timestamp (in milliseconds) when the error occurred          | 1694181328000                               |
| status    | int    | HTTP status code of the error                                     | 400                                         |
| error     | string | Brief description of the error type                               | "Bad Request"                               |
| message   | string | Detailed error message providing more information about the error | "Invalid request: missing required fields." |
| path      | string | The API endpoint path where the error occurred                    | "/payments/create-payment-intent"           |


**Error Payload Example**:
```json
{
    "timestamp": 1727169321150,
    "status": 400,
    "error": "Bad Request",
    "message": "Headers 'X-Access-Token' and 'X-Application-Id' are necessary.",
    "path": "/payments/create-payment-intent"
}
```


**HTTP Status code summary**

| Code | Status        | Description                                                                                                   |
| ---- | ------------- | ------------------------------------------------------------------------------------------------------------- |
| 200  | OK            | Everything worked as expected.                                                                                |
| 400  | Bad Request   | The request was unacceptable, often due to missing a required parameter or some auth aspect like the headers. |
| 401  | Unauthorized  | No valid pairs of auth headers was provided.                                                                  |
| 403  | Forbidden     | The client doesn’t have permissions to perform the request                                                    |
| 404  | Not Found     | The requested resource doesn’t exist.                                                                         |
| 500  | Server Errors | Something went wrong on iCliGo's end.                                                                         |


---

## **Payment Flow**

### **1. Create Payment Intent**

To initiate a payment, you first need to create a payment intent. This intent holds all the necessary information to facilitate the payment process.

**API Endpoint:**

- **Method**: POST
- **Path**: `/payments/create-payment-intent`

---

##### **Request**

This request contains all the necessary information about the payment, such as the client making the purchase, the product being bought, and additional details like success/failure URLs and whether manual capture is required.

Request DTO: [**CreateIntentRequest**](CreateIntentRequest.md)

<details>
  <summary>Basic Request Payload Example</summary>
```json
{
    "userId": "user_123",
    "productType": "BOOKING",
    "productId": "my-product-id-123",
    "products": [
        {
            "name": "Product XYZ"
        }
    ],
    "company": "icligo.pt",
    "currency": "EUR",
    "microsite": "icligo.pt",
    "country": "pt",
    "manualCapture": false,
    "successUrl": "https://success.com",
    "failureUrl": "http://failure.com",
    "amount": 100.0
}
```
</details>

<details>
  <summary>Full Payload Example</summary>
```json
{
    "clientId": "company_x_app",
    "userId": "user_1234",
    "productId": "product_1234",
    "productType": "BOOKING",
    "resume": {
        "description": "Booking a suite.",
        "reference": "REF12345678",
        "owner": "John Doe",
        "email": "johndoe@example.com",
        "currency": "EUR",
        "amount": 1500.75,
        "checkin": "2024-09-24T16:46:42.411Z",
        "checkout": "2024-09-24T16:46:42.411Z",
        "clients": [
            {
                "name": "John Doe",
                "email": "johndoe@example.com",
                "dateOfBirth": "2024-09-24T16:46:42.411Z",
                "children": false
            }
        ]
    },
    "products": [
        {
            "type": "BOOKING",
            "name": "Product XYZ",
            "location": "Location X",
            "duration": "10 Minutes",
            "code": "PRD12345",
            "transport": "CAR",
            "checkin": "2024-09-24T16:46:42.411Z",
            "checkout": "2024-09-24T16:46:42.411Z",
            "date": "2024-09-24T16:46:42.411Z",
            "price": 500,
            "detail": {
                "night": 3,
                "roomType": "Suite",
                "regime": "Half board",
                "flightNumber": "FL123",
                "departure": "2024-09-24T16:46:42.411Z",
                "arrival": "2024-09-24T16:46:42.411Z",
                "departureTime": "2024-09-24T16:46:42.411Z",
                "arrivalTime": "string",
                "departureAirport": "JFK",
                "arrivalAirport": "LHR",
                "departureCity": "New York",
                "arrivalCity": "London",
                "departureCountry": "US",
                "arrivalCountry": "UK",
                "baggage": "string",
                "duration": "string",
                "provider": "Airline XYZ",
                "reception": "string",
                "receptionTime": "2024-09-24T16:46:42.411Z",
                "destinationTime": "2024-09-24T16:46:42.411Z",
                "destination": "string",
                "circuit": [
                    {
                        "checkin": "2024-09-24T16:46:42.411Z",
                        "checkout": "2024-09-24T16:46:42.411Z",
                        "location": "string"
                    }
                ],
                "stopovers": [
                    {
                        "departure": "2024-09-24T16:46:42.411Z",
                        "arrival": "2024-09-24T16:46:42.411Z",
                        "departureTime": "2024-09-24T16:46:42.411Z",
                        "arrivalTime": "2024-09-24T16:46:42.411Z",
                        "departureAirport": "string",
                        "arrivalAirport": "string",
                        "departureCity": "string",
                        "arrivalCity": "string",
                        "departureCountry": "string",
                        "arrivalCountry": "string",
                        "duration": "2H"
                    }
                ]
            }
        }
    ],
    "currency": "EUR",
    "manualCapture": true,
    "successUrl": "https://success.com",
    "failureUrl": "http://failure.com",
    "company": "Company XYZ",
    "microsite": "site_001",
    "country": "PT",
    "amount": 100
}
```
</details>

---
##### **Responses**

**Success response (200 OK)**

The success response returns the submitted information along with additional details, such as the amounts authorized, captured, etc.

Response DTO: [**PaymentDto**](PaymentDto.md)

<details>
  <summary>Basic Response Example</summary>
```json
{
    "id": "f0824416-18d5-4fe7-8c66-7cada281c039",
    "clientId": "travel-c-app",
    "productId": "my-product-id-123",
    "productType": "BOOKING",
    "products": [
        {
            "name": "Product XYZ"
        }
    ],
    "company": "icligo.pt",
    "microsite": "icligo.pt",
    "country": "pt",
    "currency": "EUR",
    "state": "CREATED",
    "baseAmount": 100.0,
    "capturedAmount": 0,
    "authorizedAmount": 100.0,
    "refundedAmount": 0,
    "automaticCapture": false,
    "captureDetails": [],
    "refundDetails": [],
    "successUrl": "https://success.com",
    "failureUrl": "http://failure.com",
    "manualCapture": false
}
```
</details>

<details>
  <summary>Full Response Example</summary>
```json
{
    "id": "5a83701f-138a-42f1-9464-4b9ee10fc8bc",
    "clientId": "travel-c-app",
    "productId": "product_1234",
    "productType": "BOOKING",
    "resume": {
        "description": "Booking a suite.",
        "reference": "REF12345678",
        "owner": "John Doe",
        "email": "johndoe@example.com",
        "currency": "EUR",
        "amount": 1500.75,
        "checkin": "2024-09-24",
        "checkout": "2024-09-24",
        "clients": [
            {
                "name": "John Doe",
                "email": "johndoe@example.com",
                "dateOfBirth": "2024-09-24",
                "children": false
            }
        ]
    },
    "products": [
        {
            "type": "BOOKING",
            "name": "Product XYZ",
            "location": "Location X",
            "duration": "10 Minutes",
            "code": "PRD12345",
            "transport": "CAR",
            "checkin": "2024-09-24",
            "checkout": "2024-09-24",
            "date": "2024-09-24",
            "price": 500,
            "detail": {
                "night": 3,
                "roomType": "Suite",
                "regime": "Half board",
                "flightNumber": "FL123",
                "departure": "2024-09-24",
                "arrival": "2024-09-24",
                "departureTime": "2024-09-24T16:46:42.411Z",
                "arrivalTime": "string",
                "departureAirport": "JFK",
                "arrivalAirport": "LHR",
                "departureCity": "New York",
                "arrivalCity": "London",
                "departureCountry": "US",
                "arrivalCountry": "UK",
                "baggage": "string",
                "duration": "string",
                "provider": "Airline XYZ",
                "reception": "string",
                "receptionTime": "2024-09-24T16:46",
                "destinationTime": "2024-09-24T16:46",
                "destination": "string",
                "circuit": [
                    {
                        "checkin": "2024-09-24T16:46:42.411+00:00",
                        "checkout": "2024-09-24T16:46:42.411+00:00",
                        "location": "string"
                    }
                ],
                "stopovers": [
                    {
                        "departure": "2024-09-24T16:46:42.411+00:00",
                        "arrival": "2024-09-24T16:46:42.411+00:00",
                        "departureTime": "2024-09-24T16:46:42.411Z",
                        "arrivalTime": "2024-09-24T16:46:42.411Z",
                        "departureAirport": "string",
                        "arrivalAirport": "string",
                        "departureCity": "string",
                        "arrivalCity": "string",
                        "departureCountry": "string",
                        "arrivalCountry": "string",
                        "duration": "2H"
                    }
                ]
            }
        }
    ],
    "company": "Company XYZ",
    "microsite": "site_001",
    "country": "PT",
    "currency": "EUR",
    "state": "CREATED",
    "baseAmount": 100,
    "capturedAmount": 0,
    "authorizedAmount": 100,
    "refundedAmount": 0,
    "automaticCapture": true,
    "captureDetails": [],
    "refundDetails": [],
    "successUrl": "https://success.com",
    "failureUrl": "http://failure.com",
    "manualCapture": true
}
```
</details>

**Error responses**

|     |               |                                                                                                               |
| --- | ------------- | ------------------------------------------------------------------------------------------------------------- |
| 400 | Bad Request   | The request was unacceptable, often due to missing a required parameter or some auth aspect like the headers. |
| 401 | Unauthorized  | No valid pairs of auth headers was provided.                                                                  |
| 500 | Server Errors | Something went wrong on iCliGo's end.                                                                         |

---

### **2. Payment Page / Widget**

After creating the payment intent, direct the user to the payment page or widget. This part is abstracted for you. The user will complete the payment, and you will receive a webhook with the payment status: **AUTHORIZED** (for manual capture) or **COMPLETED** (for automatic capture).

!!! note

    For more information about how the widget works, please refer to the [Widget Documentation](/documentation/widget/).

---

### **3. Payment Capture (Manual vs. Automatic)**

#### **3.1 Manual Payment Flow**

If manual capture is selected, it’s necessary to proceed with the capture after the payment has been authorized. In automatic capture mode, the capture occurs automatically.

In the case of manual capture, the system will send a webhook with the **AUTHORIZED** status once the user has paid for the order. This indicates that the payment has been authorized and the amount is ready to be captured.

Afterward, it's necessary to call the `Capture` endpoint to complete the operation.

**API Endpoint:**

- **Method**: PUT
- **Path**: `/payments/{payment_id}/capture`
- **Path Variables**:
    - payment_id: The ID of the payment intent.

---

##### **Request**

The request specifies the amount to be captured and includes an optional description.

Request DTO: [**ExternalConfirmPaymentRequest**](ExternalConfirmPaymentRequest.md)

<details>
  <summary>Request Payload Example</summary>
```json
{
    "amount": 10.0,
    "description": "Captured description."
}
```
</details>

---

##### **Responses**

**Success response (200 OK)**

The response is an object detailing the date when the capture occurred, along with the captured amount presented as a list of captures.

Response DTO: [**ConfirmPaymentResponse**](ConfirmPaymentResponse.md)

!!! tip

    Although the response includes a `list` of `CaptureDetail` objects, currently only a single capture is allowed. Therefore, you can expect the list to always contain just one element.

<details>
  <summary>Response Example</summary>
```json
{
    "date": 1727193013453,
    "capturedAmountInfo": {
        "currency": "EUR",
        "value": 10.0
    },
    "captures": [
        {
            "id": "66f2df95-659b-a21d-974d-ba3b489d50d9",
            "description": "Captured by client",
            "captureTime": 1727193004172,
            "amount": {
                "currency": "EUR",
                "value": 10.0
            }
        }
    ]
}
```
</details>

!!! note

    Upon capture, a **CONFIRMED** webhook will be sent, indicating that the payment has been successfully confirmed and captured.

**Error responses**

| Code | Description  | Details                                                                                                       |
| ---- | ------------ | ------------------------------------------------------------------------------------------------------------- |
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers.     |
| 401  | Unauthorized | No valid authentication headers were provided.                                                                |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                             |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                            |

---

#### **3.2 Automatic Capture Payment Flow**

In this scenario, the **AUTHORIZED** webhook is suppressed. When the client pays for the order, a **COMPLETED** webhook is sent, indicating that the order is completed and the funds have been captured.

---

### **4. Cancel Payment**

A payment can only be canceled if its status is either **Created** or **Authorized**. Payments cannot be canceled once they are completed.

**API Endpoint:**

- **Method**: PUT
- **Path**: `/payments/{payment_id}/cancel`
- **Path Variables**:
    - payment_id: The ID of the payment intent.

---

##### **Request**

This request does not require a body. The specified payment intent will be canceled by making a PUT request to this endpoint using the provided payment_id.

---
##### **Responses**

**Success response (200 OK)**

The success response returns the cancellation date.

Request DTO: [**ExternalCancelPaymentResponse**](ExternalCancelPaymentResponse.md)
<details>
  <summary>Basic Response Example</summary>
```json
{
  "date": "1727193013453",
}
```
</details>

**Error responses**

| Code | Description  | Details                                                                                                       |
| ---- | ------------ | ------------------------------------------------------------------------------------------------------------- |
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers.     |
| 401  | Unauthorized | No valid authentication headers were provided.                                                                |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                             |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                         |

---

### 5. Refund

Refunds a payment for a given payment ID

**API Endpoint:**

- **Method**: POST
- **Path**: `/payments/{payment_id}/refund`
- **Path Variables**:
    - payment_id: The ID of the payment intent.

---

##### **Request**

The request specifies the amount to be refunded and includes an optional description.

Request DTO: [**ExternalRefundPaymentRequest**](ExternalRefundPaymentRequest.md)

<details>
  <summary>Request Payload Example</summary>
```json
{
    "amount": "10",
    "description": "Refund description."
}
```
</details>

---

##### **Responses**

**Success response (200 OK)**

The response is an object detailing the date when the refund occurred, along with the refund amount.

Response DTO: [**RefundDetail**](RefundDetail.md)

!!! tip

    Although the response includes a `list` of `RefundDetail` objects, currently only a single refund is allowed. Therefore, you can expect the list to always contain just one element.


<details>
  <summary>Response Example</summary>
```json
[
  {
      "id": "4444d000-659b-a21d-974d-ba3b489d50d9",
      "captureId": "66f2df95-659b-a21d-974d-ba3b489d50d9",
      "createTime": 1727193013453,
      "description": "Refund Description",
      "amount": {
          "currency": "EUR",
          "value": 10.0
      }
  }
]
```
</details>

**Error responses**

| Code | Description  | Details                                                                                                       |
| ---- | ------------ | ------------------------------------------------------------------------------------------------------------- |
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers.     |
| 401  | Unauthorized | No valid authentication headers were provided.                                                                |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                             |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                            |

---

### **6. Retrieve**

For a given ID retrieve all the information about the payment intent.

**API Endpoint:**

- **Method**: GET
- **Path**: `/payments/{payment_id}/retrieve`
- **Path Variables**:
    - payment_id: The ID of the payment intent.

---

##### **Request**

This request does not require a body. The specified payment intent will retrieve payment intente info by making a GET request to this endpoint using the provided payment_id.

---

##### **Responses**

**Success response (200 OK)**

The response is an object detailing the payment intent info.

Response DTO: [**ExternalPaymentDto**](ExternalPaymentDto.md)


<details>
  <summary>Response Example</summary>
```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "clientId": "string",
  "userId": "user-abc",
  "service": "Flight booking",
  "serviceDescription": "string",
  "productId": "prod-456",
  "productType": "BOOKING",
  "resume": {
    "description": "Booking a suite.",
    "reference": "REF12345678",
    "owner": "John Doe",
    "email": "johndoe@example.com",
    "currency": "EUR",
    "amount": 1500.75,
    "checkin": "2024-09-25T11:29:07.371Z",
    "checkout": "2024-09-25T11:29:07.371Z",
    "clients": [
      {
        "name": "John Doe",
        "email": "johndoe@example.com",
        "dateOfBirth": "2024-09-25T11:29:07.371Z",
        "children": false
      }
    ]
  },
  "products": [
    {
      "type": "BOOKING",
      "name": "Product XYZ",
      "location": "Location X",
      "duration": "string",
      "code": "PRD12345",
      "transport": "CAR",
      "checkin": "2024-09-25T11:29:07.371Z",
      "checkout": "2024-09-25T11:29:07.371Z",
      "date": "2024-09-25T11:29:07.371Z",
      "price": 500,
      "detail": {
        "night": 3,
        "roomType": "Suite",
        "regime": "Half board",
        "flightNumber": "FL123",
        "departure": "2024-09-25T11:29:07.371Z",
        "arrival": "2024-09-25T11:29:07.371Z",
        "departureTime": "string",
        "arrivalTime": "string",
        "departureAirport": "JFK",
        "arrivalAirport": "LHR",
        "departureCity": "New York",
        "arrivalCity": "London",
        "departureCountry": "US",
        "arrivalCountry": "UK",
        "baggage": "string",
        "duration": "string",
        "provider": "Airline XYZ",
        "reception": "string",
        "receptionTime": "2024-09-25T11:29:07.371Z",
        "destinationTime": "2024-09-25T11:29:07.371Z",
        "destination": "string",
        "circuit": [
          {
            "checkin": "2024-09-25T11:29:07.371Z",
            "checkout": "2024-09-25T11:29:07.371Z",
            "location": "string"
          }
        ],
        "stopovers": [
          {
            "departure": "2024-09-25T11:29:07.371Z",
            "arrival": "2024-09-25T11:29:07.371Z",
            "departureTime": "string",
            "arrivalTime": "string",
            "departureAirport": "string",
            "arrivalAirport": "string",
            "departureCity": "string",
            "arrivalCity": "string",
            "departureCountry": "string",
            "arrivalCountry": "string",
            "duration": "string"
          }
        ]
      }
    }
  ],
  "company": "iCliGo",
  "microsite": "iCliGo Payments",
  "country": "Spain",
  "currency": "EUR",
  "createdBy": "user-123",
  "state": "CREATED",
  "amount": 0,
  "capturedAmount": 0,
  "authorizedAmount": 0,
  "methodTax": 0,
  "captureDetails": [
    {
      "id": "string",
      "captureTime": "2024-09-25T11:29:07.371Z",
      "amount": {
        "currency": "string",
        "value": 0
      }
    }
  ],
  "refundDetails": [
    {
      "id": "string",
      "captureId": "string",
      "createTime": "2024-09-25T11:29:07.371Z",
      "description": "string",
      "amount": {
        "currency": "string",
        "value": 0
      }
    }
  ],
  "expirationDate": "2024-09-25T11:29:07.371Z"
}
```
</details>

**Error responses**

| Code | Description  | Details                                                                                                       |
| ---- | ------------ | ------------------------------------------------------------------------------------------------------------- |
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers.     |
| 401  | Unauthorized | No valid authentication headers were provided.                                                                |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                             |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                            |

---

## **Important Considerations**

- **Single Capture**: A payment can only be captured once.
- **Refunds**: Multiple refunds are allowed but the total refunded amount cannot exceed the captured amount.