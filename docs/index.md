# **iCliGo Payment API Documentation**

This API allows you to manage payment intents, enabling payment capture, cancellations, and refunds.

---

## **Authentication**

To authenticate, include the following headers with all your API requests:

- **X-Application-Id**: Your application ID.
- **X-Access-Token**: A token used to authenticate your application's access to the API.

The API will return a **400 Bad Request** response if these headers are missing or invalid. If the payment request is
associated with an unauthorized or incorrect Application ID, a **401 Unauthorised** response will be returned. If an
attempt is made to access a forbidden resource, a **403 Forbidden** response is returned.

**Test Mode Support**:

Our system supports a test mode using test credentials, where to activate this mode it is necessary to make a request
using test credentials.
The corresponding intent will be marked as a test, and all later operations must use the same test credentials.

## **Errors**

We have normalized the error payload, where all the errors obey the same format in order to be easier to read the error.

The error payload includes the following parameters:

| Parameter | Type   | Description                                                       | Example                                     |
|-----------|--------|-------------------------------------------------------------------|---------------------------------------------|
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
|------|---------------|---------------------------------------------------------------------------------------------------------------|
| 200  | OK            | Everything worked as expected.                                                                                |
| 400  | Bad Request   | The request was unacceptable, often due to missing a required parameter or some auth aspect like the headers. |
| 401  | Unauthorized  | No valid pairs of auth headers was provided.                                                                  |
| 403  | Forbidden     | The client doesn’t have permissions to perform the request                                                    |
| 404  | Not Found     | The requested resource doesn’t exist.                                                                         |
| 500  | Server Errors | Something went wrong on iCliGo's end.                                                                         |

### Field Validation

Our API provides detailed error responses for invalid or missing fields across different levels of object complexity:

- **Root-Level Field Errors**: When a required field at the top level is missing or invalid, the error message will
  specify the exact field name.
  Example: "name" is missing.
- **Nested Object Field Errors**: For fields within nested objects, the error message includes the full path to the
  field.  
  Example: `"resume.owner"` indicates an issue with the `owner` field inside the `resume` object.
- **Array Field Errors**: Errors in array elements include the specific array index and nested field path.  
  Example: `"product[1].details.night"` points to the `night` field in the details of the second product (index 1).
- **Serialization Field Errors**: Errors that occur during the serialization process, e.g., when an enumeration value is
  invalid.  
  Example: `"intentType: Value 'BOOKINx' is not valid for field 'intentType' (expected type: IntentType)"`.
- **Malformed JSON**: For errors caused by malformed JSON, the error message will be generic, stating:  
  `"Malformed JSON request"`.

Examples:

```json
{
  "timestamp": 1732807499846,
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid request payload. Reason(s): {'product[1].details.night':'Is required for product type CRUISE'}",
  "path": "/payments/create-payment-intent"
}
```

```json
{
  "timestamp": 1732810810592,
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid request payload. Reason(s): {'products.[1].detail.circuit.[0].checkin':'Value abc is not valid! Expected type: Date'}",
  "path": "/payments/create-payment-intent"
}
```

```json
{
  "timestamp": 1732810694764,
  "status": 400,
  "error": "Bad Request",
  "message": "Invalid request payload. Reason(s): {'General':'Malformed JSON request.'}",
  "path": "/payments/create-payment-intent"
}
```

---

## **Payment Flow**

### **1. Create Payment Intent**

To initiate a payment, you first need to create a payment intent. This intent holds all the necessary information to
facilitate the payment process.

**API Endpoint:**

- **Method**: POST
- **Path**: `/payments/create-payment-intent`

---

##### **Request**

This request contains all the necessary information about the payment, such as the client making the purchase, the
product being bought, and additional details like success/failure URLs and whether manual capture is required.

!!! note

    To create a test intent make the request with the test credentials.

!!! note

The product array can accommodate various product types. The following example demonstrates an intent with one of all
available products. For detailed payload information, please refer to the specific ProductDto documentation.

Request DTO: [**CreateIntentRequest**](CreateIntentRequest.md)

<details>
  <summary>Request Payload Example With All Products</summary>
```json
{
  "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
  "userEmail": "joedoe@email.com",
  "userContact": "+351 910 000 000",
  "userName": "Joe Doe",
  "cancellationFees": [
    {
      "limitDate": "2000-12-12",
      "price": "10.00"
    }
  ],
  "cancellationFeesStrings": [
    "Non-refundable.",
    "Refundable until 12-12-2000 with a fee of 10.00.",
    "string ...."
  ],
  "resume": {
    "owner": "Bob Smith",
    "clients": [
      {
        "name": "Name 1",
        "email": "email@email.com",
        "dateOfBirth": "2000-10-10",
        "children": false
      },
      {
        "name": "Name 2",
        "email": "email2@email.com",
        "dateOfBirth": "2000-10-10",
        "children": false
      }
    ]
  },
  "intentType": "BOOKING",
  "productId": "my-product-id-123",
  "products": [
    {
      "type": "FLIGHT",
      "name": "TAP air PORTUGAL",
      "checkin": "2024-12-04",
      "importantInfo": "Important notes ...",
      "detail": {
        "flightNumber": "1234546",
        "departure": "2024-12-05",
        "arrival": "2024-12-20",
        "departureTime": "10:00",
        "arrivalTime": "16:00",
        "departureAirport": "OPO",
        "arrivalAirport": "IST",
        "departureCity": "Porto",
        "arrivalCity": "Istanbul",
        "departureCountry": "Portugal",
        "arrivalCountry": "Turkey",
        "baggage": "1",
        "duration": "4h"
      }
    },
    {
      "type": "CRUISE",
      "name": "cruise name",
      "checkin": "2024-12-15",
      "importantInfo": "Important notes ...",
      "detail": {
        "night": 9,
        "roomType": "OCEAN_VIEW",
        "regime": "all-inclusive",
        "circuit": [
          {
            "checkin": "2024-12-11T11:03:42.501+00:00",
            "checkout": "2024-12-11T11:03:42.501+00:00",
            "location": "Turkey"
          },
          {
            "checkin": "2024-12-20T11:03:42.501+00:00",
            "checkout": "2024-12-20T11:03:42.501+00:00",
            "location": "Turkey"
          }
        ]
      }
    },
    {
      "type": "TRANSFER",
      "name": "BUS 309",
      "location": "Istanbul",
      "transport": "BUS",
      "checkin": "2024-12-20",
      "checkout": "2024-12-20",
      "importantInfo": "Important notes ...",
      "detail": {
        "provider": "Istanbul Transfers",
        "reception": "Crowne Plaza: Istanbul - Old City",
        "receptionTime": "2024-09-20T16:00",
        "destinationTime": "2024-09-20T16:15",
        "destination": "Istanbul Airport"
      }
    },
    {
      "type": "ACTIVITY",
      "name": "Activity's name",
      "location": "Istanbul",
      "duration": "3h",
      "checkin": "2024-12-15",
      "checkout": "2024-12-15",
      "importantInfo": "Important notes ..."
    },
    {
      "type": "INSURANCE",
      "name": "Seguro XYZ",
      "price": 12,
      "importantInfo": "Important notes ..."
    },
    {
      "type": "EVENT",
      "name": "Event's name",
      "location": "Istanbul",
      "checkin": "2021-12-01",
      "checkout": "2021-12-10",
      "importantInfo": "Important notes ..."
    },
    {
      "type": "ACCOMMODATION",
      "name": "Hotel's name",
      "location": "Istanbul",
      "checkin": "2024-12-05",
      "checkout": "2024-12-20",
      "importantInfo": "Important notes ...",
      "detail": {
        "night": 9,
        "roomType": "OCEAN_VIEW",
        "regime": "all-inclusive"
      }
    }
  ],
  "company": "icligo.pt",
  "currency": "EUR",
  "microsite": "icligo.pt",
  "country": "pt",
  "manualCapture": true,
  "successUrl": "https://success.com",
  "failureUrl": "https://failure.com",
  "ideaId": "15847300",
  "amount": 100.0,
  "totalAmountService": 2500.00
}
```
</details>

---

##### **Responses**

**Success response (200 OK)**

The success response returns the submitted information along with additional details, such as the amounts authorized,
captured, etc.

Response DTO: [**ExternalPaymentDto**](ExternalPaymentDto.md)

<details>
  <summary>Response Example With All Products</summary>
```json
{
    "id": "b91c35cc-db74-4663-a491-bed750686faa",
    "clientId": "travel-c-app-test",
    "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
    "productId": "my-product-id-123",
    "intentType": "BOOKING",
    "resume": {
        "owner": "Bob Smith",
        "clients": [
            {
                "name": "Name 1",
                "email": "email@email.com",
                "dateOfBirth": "2000-10-10",
                "children": false
            },
            {
                "name": "Name 2",
                "email": "email2@email.com",
                "dateOfBirth": "2000-10-10",
                "children": false
            }
        ]
    },
    "products": [
        {
            "type": "FLIGHT",
            "name": "TAP air PORTUGAL",
            "checkin": "2024-12-04",
            "detail": {
                "flightNumber": "1234546",
                "departure": "2024-12-05",
                "arrival": "2024-12-20",
                "departureTime": "10:00",
                "arrivalTime": "16:00",
                "departureAirport": "OPO",
                "arrivalAirport": "IST",
                "departureCity": "Porto",
                "arrivalCity": "Istanbul",
                "departureCountry": "Portugal",
                "arrivalCountry": "Turkey",
                "baggage": "1",
                "duration": "4h"
            },
            "importantInfo": "Important notes ..."
        },
        {
            "type": "CRUISE",
            "name": "cruise name",
            "checkin": "2024-12-15",
            "detail": {
                "night": 9,
                "roomType": "OCEAN_VIEW",
                "regime": "all-inclusive",
                "circuit": [
                    {
                        "checkin": "2024-12-11T11:03:42.501+00:00",
                        "checkout": "2024-12-11T11:03:42.501+00:00",
                        "location": "Turkey"
                    },
                    {
                        "checkin": "2024-12-20T11:03:42.501+00:00",
                        "checkout": "2024-12-20T11:03:42.501+00:00",
                        "location": "Turkey"
                    }
                ]
            },
            "importantInfo": "Important notes ..."
        },
        {
            "type": "TRANSFER",
            "name": "BUS 309",
            "location": "Istanbul",
            "transport": "BUS",
            "checkin": "2024-12-20",
            "checkout": "2024-12-20",
            "detail": {
                "provider": "Istanbul Transfers",
                "reception": "Crowne Plaza: Istanbul - Old City",
                "receptionTime": "2024-09-20T16:00",
                "destinationTime": "2024-09-20T16:15",
                "destination": "Istanbul Airport"
            },
            "importantInfo": "Important notes ..."
        },
        {
            "type": "ACTIVITY",
            "name": "Activity's name",
            "location": "Istanbul",
            "duration": "3h",
            "checkin": "2024-12-15",
            "checkout": "2024-12-15",
            "importantInfo": "Important notes ..."
        },
        {
            "type": "INSURANCE",
            "name": "Seguro XYZ",
            "price": 12,
            "importantInfo": "Important notes ..."
        },
        {
            "type": "EVENT",
            "name": "Event's name",
            "location": "Istanbul",
            "checkin": "2021-12-01",
            "checkout": "2021-12-10",
            "importantInfo": "Important notes ..."
        },
        {
            "type": "ACCOMMODATION",
            "name": "Hotel's name",
            "location": "Istanbul",
            "checkin": "2024-12-05",
            "checkout": "2024-12-20",
            "detail": {
                "night": 9,
                "roomType": "OCEAN_VIEW",
                "regime": "all-inclusive"
            },
            "importantInfo": "Important notes ..."
        }
    ],
    "company": "icligo.pt",
    "microsite": "icligo.pt",
    "country": "pt",
    "currency": "EUR",
    "state": "CREATED",
    "amount": 100.0,
    "totalAmountService": 2500.00,
    "capturedAmount": 0,
    "authorizedAmount": 0,
    "refundedAmount": 0,
    "manualCapture": true,
    "captureDetails": [],
    "refundDetails": [],
    "successUrl": "https://success.com",
    "failureUrl": "https://failure.com",
    "testMode": true
}
```
</details>

**Error responses**

|     |               |                                                                                                               |
|-----|---------------|---------------------------------------------------------------------------------------------------------------|
| 400 | Bad Request   | The request was unacceptable, often due to missing a required parameter or some auth aspect like the headers. |
| 401 | Unauthorized  | No valid pairs of auth headers was provided.                                                                  |
| 500 | Server Errors | Something went wrong on iCliGo's end.                                                                         |

---

### **2. Payment Page / Widget**

After creating the payment intent, direct the user to the payment page or widget. This part is abstracted for you. The
user will complete the payment, and you will receive a webhook with the payment status: **AUTHORIZED** (for manual
capture) or **COMPLETED** (for automatic capture).

!!! note

    For more information about how the widget works, please refer to the [Widget Documentation](/documentation/widget/).

---

### **3. Payment Capture (Manual vs. Automatic)**

#### **3.1 Manual Payment Flow**

If manual capture is selected, it’s necessary to proceed with the capture after the payment has been authorized. In
automatic capture mode, the capture occurs automatically.

In the case of manual capture, the system will send a webhook with the **AUTHORIZED** status once the user has paid for
the order. This indicates that the payment has been authorized and the amount is ready to be captured.

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

The response is an object detailing the date when the capture occurred, along with the captured amount presented as a
list of captures.

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

    Upon capture, a **COMPLETED** webhook will be sent, indicating that the payment has been successfully confirmed and captured.

**Error responses**

| Code | Description  | Details                                                                                                    |
|------|--------------|------------------------------------------------------------------------------------------------------------|
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers. |
| 401  | Unauthorized | No valid authentication headers were provided.                                                             |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                         |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                        |

---

#### **3.2 Automatic Capture Payment Flow**

In this scenario, the **AUTHORIZED** webhook is suppressed. When the client pays for the order, a **COMPLETED** webhook
is sent, indicating that the order is completed and the funds have been captured.

---

### **4. Cancel Payment**

A payment can only be canceled if its status is either **Created** or **Authorized**. Payments cannot be canceled once
they are completed.

**API Endpoint:**

- **Method**: PUT
- **Path**: `/payments/{payment_id}/cancel`
- **Path Variables**:
    - payment_id: The ID of the payment intent.

---

##### **Request**

This request does not require a body. The specified payment intent will be canceled by making a PUT request to this
endpoint using the provided payment_id.

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

| Code | Description  | Details                                                                                                    |
|------|--------------|------------------------------------------------------------------------------------------------------------|
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers. |
| 401  | Unauthorized | No valid authentication headers were provided.                                                             |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                         |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                        |

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

| Code | Description  | Details                                                                                                    |
|------|--------------|------------------------------------------------------------------------------------------------------------|
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers. |
| 401  | Unauthorized | No valid authentication headers were provided.                                                             |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                         |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                        |

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

This request does not require a body. The specified payment intent will retrieve payment intent info by making a GET
request to this endpoint using the provided payment_id.

---

##### **Responses**

**Success response (200 OK)**

The response is an object detailing the payment intent info.

Response DTO: [**ExternalPaymentDto**](ExternalPaymentDto.md)

<details>
  <summary>Response Example With All Products</summary>
```json
{
    "id": "b91c35cc-db74-4663-a491-bed750686faa",
    "clientId": "travel-c-app-test",
    "userId": "5c6bd4ff-fe65-4899-ac50-af305c27f86d",
    "productId": "my-product-id-123",
    "intentType": "BOOKING",
    "resume": {
        "owner": "Bob Smith",
        "clients": [
            {
                "name": "Name 1",
                "email": "email@email.com",
                "dateOfBirth": "2000-10-10",
                "children": false
            },
            {
                "name": "Name 2",
                "email": "email2@email.com",
                "dateOfBirth": "2000-10-10",
                "children": false
            }
        ]
    },
    "products": [
        {
            "type": "FLIGHT",
            "name": "TAP air PORTUGAL",
            "checkin": "2024-12-04",
            "detail": {
                "flightNumber": "1234546",
                "departure": "2024-12-05",
                "arrival": "2024-12-20",
                "departureTime": "10:00",
                "arrivalTime": "16:00",
                "departureAirport": "OPO",
                "arrivalAirport": "IST",
                "departureCity": "Porto",
                "arrivalCity": "Istanbul",
                "departureCountry": "Portugal",
                "arrivalCountry": "Turkey",
                "baggage": "1",
                "duration": "4h"
            },
            "importantInfo": "Important notes ..."
        },
        {
            "type": "CRUISE",
            "name": "cruise name",
            "checkin": "2024-12-15",
            "detail": {
                "night": 9,
                "roomType": "OCEAN_VIEW",
                "regime": "all-inclusive",
                "circuit": [
                    {
                        "checkin": "2024-12-11T11:03:42.501+00:00",
                        "checkout": "2024-12-11T11:03:42.501+00:00",
                        "location": "Turkey"
                    },
                    {
                        "checkin": "2024-12-20T11:03:42.501+00:00",
                        "checkout": "2024-12-20T11:03:42.501+00:00",
                        "location": "Turkey"
                    }
                ]
            },
            "importantInfo": "Important notes ..."
        },
        {
            "type": "TRANSFER",
            "name": "BUS 309",
            "location": "Istanbul",
            "transport": "BUS",
            "checkin": "2024-12-20",
            "checkout": "2024-12-20",
            "detail": {
                "provider": "Istanbul Transfers",
                "reception": "Crowne Plaza: Istanbul - Old City",
                "receptionTime": "2024-09-20T16:00",
                "destinationTime": "2024-09-20T16:15",
                "destination": "Istanbul Airport"
            },
            "importantInfo": "Important notes ..."
        },
        {
            "type": "ACTIVITY",
            "name": "Activity's name",
            "location": "Istanbul",
            "duration": "3h",
            "checkin": "2024-12-15",
            "checkout": "2024-12-15",
            "importantInfo": "Important notes ..."
        },
        {
            "type": "INSURANCE",
            "name": "Seguro XYZ",
            "price": 12,
            "importantInfo": "Important notes ..."
        },
        {
            "type": "EVENT",
            "name": "Event's name",
            "location": "Istanbul",
            "checkin": "2021-12-01",
            "checkout": "2021-12-10",
            "importantInfo": "Important notes ..."
        },
        {
            "type": "ACCOMMODATION",
            "name": "Hotel's name",
            "location": "Istanbul",
            "checkin": "2024-12-05",
            "checkout": "2024-12-20",
            "detail": {
                "night": 9,
                "roomType": "OCEAN_VIEW",
                "regime": "all-inclusive"
            },
            "importantInfo": "Important notes ..."
        }
    ],
    "company": "icligo.pt",
    "microsite": "icligo.pt",
    "country": "pt",
    "currency": "EUR",
    "state": "CREATED",
    "amount": 100.0,
    "totalAmountService": 2500.00,
    "capturedAmount": 0,
    "authorizedAmount": 0,
    "refundedAmount": 0,
    "manualCapture": true,
    "captureDetails": [],
    "refundDetails": [],
    "successUrl": "https://success.com",
    "failureUrl": "https://failure.com",
    "testMode": true
}
```
</details>

**Error responses**

| Code | Description  | Details                                                                                                    |
|------|--------------|------------------------------------------------------------------------------------------------------------|
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers. |
| 401  | Unauthorized | No valid authentication headers were provided.                                                             |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                         |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                        |

---

## **Important Considerations**

- **Single Capture**: A payment can only be captured once.
- **Refunds**: Multiple refunds are allowed, but the total refunded amount cannot exceed the amount of intent.