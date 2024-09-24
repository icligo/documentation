# **iCliGo Payment API Documentation**

This API allows you to manage payment intents, enabling payment capture, cancellations and refunds. 

---

## **Authentication**

To authenticate, include the following headers with your API requests:
- **X-Application-Id**: Your application ID.
- **X-Access-Token**: A token used to authenticate your application's access to the API.

The API will return a **400 Bad Request** response if these headers are missing or invalid. If the payment request is associated with an unauthorised or incorrect Application ID, a **401 Unauthorised** response will be returned. If an attempt is made to access a forbidden resource, a **403 Forbidden** response is returned.

---

## **Errors**
We have normalized the error payload, where all the errors obey the same format in order to be easier to read the error.

The error payload includes the following parameters:
- timestamp
- status
- error
- message
- path

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

To initiate a payment, you first need to create a payment intent. This intent holds the necessary information for the payment process.

**API Endpoint:**

- **Method**: POST
- **Path**: `/payments/create-payment-intent`

---

#### **Request**

TODO: Add description context

[**CreateIntentRequest**](CreateIntentRequest.md)

<details>
  <summary>Basic Request Payload Example</summary>
```json
{
  "userId": "user_1234",
  "productId": "product_1234",
  "productType": "BOOKING",
  "products": [
    {
      "id": "prod_001",
      "name": "Hotel Room",
      "quantity": 1,
      "price": {
        "currency": "EUR",
        "value": 100.00
      }
    }
  ],
  "company": "icligo.pt",
  "currency": "EUR",
  "microsite": "icligo.pt",
  "country": "PT",
  "amount": 25.0
  "manualCapture": false
}
```
</details>

<details>
  <summary>Full Payload Example</summary>
```json
{
  "userId": "user_1234",
  "productId": "product_1234",
  "productType": "BOOKING",
  "products": [
    {
      "id": "prod_001",
      "name": "Hotel Room",
      "quantity": 1,
      "price": {
        "currency": "EUR",
        "value": 100.00
      }
    }
  ],
  "company": "icligo.pt",
  "currency": "EUR",
  "microsite": "icligo.pt",
  "country": "PT",
  "amount": 25.0
  "manualCapture": false
}
```
</details>

---
#### **Responses**

**Success response (200 OK)**

TODO: Add description context

[**PaymentDto**](PaymentDto.md)

<details>
  <summary>Response Example</summary>
```json
{
  "userId": "user_1234",
  "productId": "product_1234",
  "productType": "BOOKING",
  "products": [
    {
      "id": "prod_001",
      "name": "Hotel Room",
      "quantity": 1,
      "price": {
        "currency": "EUR",
        "value": 100.00
      }
    }
  ],
  "company": "icligo.pt",
  "currency": "EUR",
  "microsite": "icligo.pt",
  "country": "PT",
  "amount": 25.0
  "manualCapture": false
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

---

### 3. Payment Capture (Manual vs. Automatic)

#### 3.1 Manual Payment Flow

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

> [!TIP]
> Although the response includes a `list` of `CaptureDetail` objects, currently only a single capture is allowed. Therefore, you can expect the list to always contain just one element.

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

> [!NOTE]  
> Upon capture, a **CONFIRMED** webhook will be sent, indicating that the payment has been successfully confirmed and captured.

**Error responses**

| Code | Description  | Details                                                                                                       |
| ---- | ------------ | ------------------------------------------------------------------------------------------------------------- |
| 400  | Bad Request  | The request was unacceptable, often due to missing required parameters or incorrect authorization headers.     |
| 401  | Unauthorized | No valid authentication headers were provided.                                                                |
| 403  | Forbidden    | The client lacks the necessary permissions to perform the request.                                             |
| 500  | Server Error | An issue occurred on iCliGo’s side.                                                                            |

---

#### 3.2 Automatic Capture Payment Flow

In this scenario, the **AUTHORIZED** webhook is suppressed. When the client pays for the order, a **COMPLETED** webhook is sent, indicating that the order is completed and the funds have been captured.

---

### **4. Cancel Payment**

Cancel a payment only when its status is either **Created** or **Authorized**. Payments cannot be canceled once completed.


---

### **5. Refund Payment**

A payment can only be refunded if it is in the **Completed** state. Refunds can be partial or full, and multiple refunds are allowed until the total refunded amount equals the original captured amount.

---

## **Important Considerations**

- **Single Capture**: A payment can only be captured once.
- **Refunds**: Multiple refunds are allowed but the total refunded amount cannot exceed the captured amount.