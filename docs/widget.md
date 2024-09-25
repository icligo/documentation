# Payment Gateway Widget

This widget is a custom payment form built using **iCligoPaymentGateway**. It renders a payment form on the web page, leveraging a React-based component bundled in `index.umd.js`.



```plain
https://staging.icligo.com/payment-gateway/widgets/styles/style.css
https://staging.icligo.com/payment-gateway/widgets/index.umd.js
```



**Prerequisites**

`paymentId`: Unique identifier for the payment session (e.g., `'54727d94-3b4e-4fa1-b356-38e0eb6ecdaa'`).



**WIDGET**

The widget is initialised inside the custom HTML tag `<icligo-widget-app>`. The `data-widget` attribute defines the widget type (`payment-form` in this case).

```xml
<!-- Widget container -->
<icligo-widget-app data-widget="payment-form"></icligo-widget-app>
```



The script passes in a set of props to the `payment-form` widget:

*   `paymentId`: Unique identifier for the payment session (e.g., `'54727d94-3b4e-4fa1-b356-38e0eb6ecdaa'`).
*   `options`: Configuration options for the widget:
    *   `locale`: Locale setting (e.g., `'pt'` for Portuguese, `'en'` , `'it'`, `'de'`, `'es'`).
    *   `showCopyButton`: Boolean to toggle the display of a button that allows users to copy payment details.

![](https://t42104168.p.clickup-attachments.com/t42104168/6fe09fbe-94f9-425e-bfaf-2fcc10a1917d/Screenshot%202024-09-24%20at%2017.17.32.png)

*       *   `vouchers`: Boolean to determine if vouchers are enabled (in this case, disabled).

!!! example

    ``` javascript
    const props = {
            paymentId: '54727d94-3b4e-4fa1-b356-38e0eb6ecdaa',
            options: {
                locale: 'pt',
                showCopyButton: true,
                vouchers: true
            }
            };
    ```



Full Demo html

```xml
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <!-- Widget styles -->
    <link
      rel="stylesheet"
      href="https://staging.icligo.com/payment-gateway/widgets/styles/style.css"
      data-asset-type="stylesheet" />
    <!-- Widget library -->
    <script
      type="application/javascript"
      src="https://staging.icligo.com/payment-gateway/widgets/index.umd.js"></script>
  </head>
  <body>
    <div style="max-width: 768px; margin: 0 auto">
      <!-- Widget container -->
      <icligo-widget-app data-widget="payment-form"></icligo-widget-app>
    </div>

    <!-- browser -->
    <script type="application/javascript">
      ((widget) => {
        const props = {
          paymentId: 'ebe304bb-d8a9-4542-b8e1-9c1ea85e7cdc',
          options: {
            locale: 'pt',
            showCopyButton: true,
            vouchers: true
          }
        };
        widget('payment-form', props);
      })(window.iCligoPaymentGateway.widgets.PaymentForm);
    </script>
  </body>
</html>
```



![](https://t42104168.p.clickup-attachments.com/t42104168/147ef0fb-0bbe-4acb-82e1-616a71b29dd3/image.png)



This widget also can be called by url: `/payment-gateway?payment=8037c4e1-7075-4fc4-94c2-dace98d49ab6&enableCopy=false&enableVouchers=false`







*   This page can be called by url: `https://staging.icligo.com/payment-gateway/payment-gateway?payment=8037c4e1-7075-4fc4-94c2-dace98d49ab6`



```plain
enableCopy
enableVouchers
```





![](https://t42104168.p.clickup-attachments.com/t42104168/cb336be4-e895-471d-b5f0-b75f18f2f05a/image.png)
