# **Test Payment Methods**

This page provides instructions on testing different payment methods in a controlled environment. Each method is categorized based on its flow (inline form or external redirection).

---

## Payment Methods

### **1. Inline Form Payment**

For payment methods where card details are entered directly in an inline form, use the following test cards:

| **3D Secure usage** | **Outcome** | **Test Card Number** |
|---------------------|-------------|----------------------|
| 3DS Required        | OK          | 4000 0000 0000 3220  |
| 3DS Required        | Declined    | 4000 0084 0000 1629  |
| 3DS Required        | Error       | 4000 0084 0000 1280  |
| 3DS Supported       | OK          | 4000 0000 0000 3220  |
| 3DS Supported       | Error       | 4000 0000 0000 3097  |
| 3DS Supported       | Unenrolled  | 4242 4242 4242 4242  |
| 3DS Not supported   | -           | 3782 822463 10005    |

These cards simulate different scenarios for **Stripe** integration.

---

### **2. External Payment Redirect**

For payment methods that redirect to an external page (e.g., a new tab or window), use the following guidelines:

#### **Viva Wallet**
1. When redirected, use Viva Wallet's test environment.
2. Follow their documentation for test credentials and flows:  
   [Viva Wallet Test Cards](https://developer.viva.com/integration-reference/test-cards-and-environments/)

#### **Revolut**
1. When redirected, use Revolut's sandbox environment.
2. Follow their guidelines for simulating transactions:  
   [Revolut Test Cards](https://developer.revolut.com/docs/guides/accept-payments/get-started/test-implementation/test-cards)

#### **PayPal**
1. When redirected, log in using the following sandbox test credentials:
    - **Email**: `sb-74kmc30573880@personal.example.com`
    - **Password**: `Z^rbNKj5`
2. Approve the transaction to complete the test payment.

---

### Notes:

1. These test payment methods and cards must only be used in a test environment.
2. Ensure your system is configured to handle redirections correctly for external payments.
3. Inline form integrations like **Stripe** should validate card data securely and comply with PCI standards.
4. Misuse of test credentials or cards in production environments may result in account suspension or violations.
