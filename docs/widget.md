# **Payment Gateway Widget**

Documentation for iCliGo’s payment platform.

There are two ways to present the payment interface:

1. Widget
2. External Page

## **Prerequisite**

To initiate a payment, a payment intent (***paymentId***) must be created beforehand.

In this documentation, we will use the following session as an example.

```jsx
const paymentId = '54727d94-3b4e-4fa1-b356-38e0eb6ecdaa';
```

## **Widget Mode**

Use the widget mode to embed the form into an existing page.

### **Assets**

CSS and Script to include in the html page.

```html
<!-- Widget styles -->
<link
  rel="stylesheet"
  href="https://staging.icligo.com/payment-gateway/widgets/styles/style.css"
  data-asset-type="stylesheet"
/>
<!-- Widget library -->
<script
  type="application/javascript"
  src="https://staging.icligo.com/payment-gateway/widgets/index.umd.js"
></script>
```

### **Initialise Widget**

To initialise the Widget, include the assets defined above and:

1. Include the HTML element where the widget is loaded (container).

    ```html
    <!-- Widget container -->
    <icligo-widget-app data-widget="payment-form"></icligo-widget-app>
    ```

      **Attributes**
   
      | Attribute | Required | Description |
          | --- | --- | --- |
      | `data-widget` | *true* | Unique element ID |
   


2. Execute function P*aymentForm* (*window.iCligoPaymentGateway.widgets.PaymentForm*)

    ```html
    <!-- Start Widget -->
    <script type="application/javascript">
      ((widget) => {
        const props = {
          paymentId: '54727d94-3b4e-4fa1-b356-38e0eb6ecdaa',
          options: {
            locale: 'pt',
            showCopyButton: true,
            vouchers: true
          }
        };
        widget('payment-form', props);
      })(window.iCligoPaymentGateway.widgets.PaymentForm);
    </script>
    ```

      ***PaymentForm Args***
   
       ```javascript
       window.iCligoPaymentGateway.widgets.PaymentForm(containerId, props)
       ```
   
      | Arg                              | Type                                    | Required | Default | Description |
          |----------------------------------|-----------------------------------------| --- | --- | --- |
      | *`containerId`*                  | *string*                                | *true* |  | ID defined on HTML element attribute (`data-widget`)  |
      | *`props`*                        | *object*                                | true |  | Widget Props |
      | *`props.paymentId`*              | string                                  | *true* |  | Payment intent ID |
      | *`props.options`*                | *object*                                | *false* |  | Widget options |
      | *`props.options.locale`*         | *Enum* <br/> `"pt","en","es","fr","it"` | *false* | `"pt"` | Widget locale definitions |
      | *`props.options.showCopyButton`* | *boolean*                               | *false* | `true` | Show button ‘copy payment link’ |
      | *`props.options.vouchers`*       | *boolean*                               | *false* | `true` | Show voucher’s section |

### **Widget Example**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <!-- Widget styles -->
    <link
      rel="stylesheet"
      href="https://staging.icligo.com/payment-gateway/widgets/styles/style.css"
      data-asset-type="stylesheet"
    />
    <!-- Widget library -->
    <script
      type="application/javascript"
      src="https://staging.icligo.com/payment-gateway/widgets/index.umd.js"
    ></script>
  </head>
  <body>
    <div style="max-width: 768px; margin: 0 auto">
      <!-- Widget container -->
      <icligo-widget-app data-widget="payment-form"></icligo-widget-app>
    </div>

    <!-- Start Widget -->
    <script type="application/javascript">
      ((widget) => {
        const props = {
          paymentId: '54727d94-3b4e-4fa1-b356-38e0eb6ecdaa',
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

![](assets/widget.png){ width="580" }

## **External Page (full page url)**

Open the platform on a new page.

### **URL address**

```html
https://staging.icligo.com/payment-gateway?payment={paymentId}&enableCopy=true&enableVouchers=true
```

### **URL Params**

| Attribute         | Required | Default | Description |
|-------------------| --- | --- | --- |
| *`payment`*       | *true* |  | Payment intent ID |
| *`enableCopy`*    | *false* | *true* | Show button ‘copy payment link’ |
| *`enableVouchers`* | *false* | *true* | Show voucher’s section |

![](assets/page.png){ width="768" }
