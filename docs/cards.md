# **Test Cards**

This page provides instructions on using test cards for simulating payments in a controlled environment, based on the product type and transaction value.

---

## Product Type: `booking`

For products of type `booking`, use the following guidelines based on the transaction amount (`amount`):

### **1. Transactions with `amount >= 20`**

| **Selected Method** | **Test Card Number** |
|-------------------------|----------------------|
| Visa                    | 4147 4630 1111 0133	  |
| American Express        | 4000 0000 0000 3220  |
| Mastercard              | 5281 4388 0180 4148  |

### **2. Transactions with `0 < amount < 20`**

Payments with these values do not support card transactions.

### **3. Transactions with `amount == 0`**

Payments with these values do not support card transactions.

---

### **PayPal Payments**

If the selected payment method is **PayPal**, follow these steps for testing:
1. When redirected to PayPal's login page, use the following test credentials:
    - **Email**: `sb-74kmc30573880@personal.example.com`
    - **Password**: `Z^rbNKj5`

2. After logging in, approve the transaction to simulate a successful payment.

**Note**: Ensure the test environment is correctly configured to use PayPal's sandbox API.


### Notes:

1. These test cards should only be used in a test environment.
2. Make sure to handle card data securely and comply with relevant regulations.
3. Any misuse of test cards in production environments may result in errors or violations.
