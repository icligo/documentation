# **Webhooks**

This document describes our strategies for ensuring reliable webhook delivery to our clients. It details the methods we employ to guarantee the integrity and confidentiality of webhook transmissions, the structure of the payload we send, and the process for confirming successful delivery of the webhooks.

---

## **Content**
- [Payload Structure](#payload-structure)
- [Security and Verification](#security-and-verification)
- [Webhook Delivery Confirmation](#webhook-delivery-confirmation)

---

## **Payload Structure**

The webhook payload consists of two main parts:

1. **payload**: Contains the event details.
2. **metadata**: Contains additional information for verifying the authenticity of the payload.

An example payload is shown below:

```json
{
  "payload": {
    "event": "PAYMENT_AUTHORIZED",
    "reference": "your-product-reference",
    "payment-id": "payment-order-id"
  },
  "metadata": {
    "signature": "CxyPzcjL9SPiXZGFpKp+/p6Lj1GciIQ3owm{...}fgULDtJ3YUsdweCirc9IJf2VEO4gBwEV2xw==",
    "timestamp": "1721317618422",
    "keyword": "secret-key"
  }
}
```

---
## **Fields**

### **Payload**

The payload contains information about the event and has a consistent format across all events.

| Field      | Description                              | Type   |
| ---------- | ---------------------------------------- | ------ |
| event      | The type of event being reported.        | String |
| reference  | The client's reference.                  | String |
| payment-id | Our unique payment order identification. | String |

The possible events are:

- **PAYMENT_AUTHORIZED**: The payment is authorized.
- **PAYMENT_COMPLETED**: The payment it was completed (captured).
- **PAYMENT_CANCELLED**: The payment was cancelled.

### **Metadata**

The metadata contains information for verifying the authenticity of the payload.

| Field     | Description                                                             | Type   |
| --------- | ----------------------------------------------------------------------- | ------ |
| signature | A base64 RSA digital signature.                                         | String |
| timestamp | The timestamp when the payload was created, in Unix epoch milliseconds. | String |
| keyword   | An agreed-upon secret keyword.                                          | String |

---

## **Security and Verification**

To verify the authenticity of the webhooks, we employ two strategies: the Keyword strategy and the Signature strategy.

### **Keyword Strategy**

This straightforward strategy involves using an agreed-upon keyword to verify the authenticity of the payload.

**Steps to Verify:**

1. **Save the keyword:** Store the agreed-upon keyword.
2. **Compare the keyword:** When receiving the request, compare the keyword in the payload with the stored keyword to ensure they match.

### **Signature Strategy**

This more secure strategy involves digital signatures and RSA public keys.

**Steps to Verify:**

1. **Save the public key:** After subscribing to our webhooks, you will receive an RSA public key in the PKCS8 format. Store this key securely.
2. **Hash the payload:**
    - Remove all spaces from the raw payload to normalize it.

      *Raw payload:*
      ```json
      {
        "event": "PAYMENT_AUTHORIZED",
        "reference": "reference-id",
        "payment-id": "d76d1fcb-9a9e-489b-a71b-25304c2d8c5c"
      }
      ```

      *Processed payload:*
      ```json
      {"event":"PAYMENT_AUTHORIZED","reference":"reference-id","payment-id":"d76d1fcb-9a9e-489b-a71b-25304c2d8c5c"}
      ```
    - Generate a SHA-256 hash of the processed payload. For example:
      ```
      e9f77536b9fc6ec2853fdd4d0026ca29541e741b225d8ce9107e612350149a15
      ```
3. **Verify the signature:** Use the stored public key, the generated payload hash, and the signature provided in the metadata to verify the signature.

    - Load the public key into the program.
    - Verify the signature using the `SHA512 RSA` algorithm.

!!! note

    Be careful to use the correct algorithms! The signature is using `SHA512 RSA`, the public key is in the `PKCS8` format, and the hash is generated with `SHA-256`.


**Example Code of Signature Strategy**

=== "Java"

    ``` java
    import java.nio.charset.StandardCharsets;
    import java.security.KeyFactory;
    import java.security.MessageDigest;
    import java.security.PublicKey;
    import java.security.Signature;
    import java.security.spec.X509EncodedKeySpec;
    import java.util.Base64;

    class PayloadValidation {

        private static PublicKey parsePublicKey(String publicKeyString) throws Exception {
            publicKeyString = publicKeyString
                    .replace("\n", "")
                    .replace("-----END PUBLIC KEY-----", "")
                    .replace("-----BEGIN PUBLIC KEY-----", "");

            byte[] publicKeyBytes = Base64.getDecoder().decode(publicKeyString);
            X509EncodedKeySpec keySpec = new X509EncodedKeySpec(publicKeyBytes);
            KeyFactory keyFactory = KeyFactory.getInstance("RSA");
            return keyFactory.generatePublic(keySpec);
        }

        private static boolean verifyMessage(String publicKeyStr, String plainText, String signature) throws Exception {
            Signature publicSignature = Signature.getInstance("SHA512withRSA");
            PublicKey publicKey = parsePublicKey(publicKeyStr);
            publicSignature.initVerify(publicKey);
            publicSignature.update(plainText.getBytes(StandardCharsets.UTF_8));
            byte[] signatureBytes = Base64.getDecoder().decode(signature);
            return publicSignature.verify(signatureBytes);
        }

        public static String generateSHA256Hash(String string) throws Exception {
            MessageDigest digest = MessageDigest.getInstance("SHA-256");
            byte[] encodedHash = digest.digest(string.getBytes(StandardCharsets.UTF_8));
            return bytesToHex(encodedHash);
        }

        private static String bytesToHex(byte[] hash) {
            StringBuilder hexString = new StringBuilder(2 * hash.length);
            for (byte b : hash) {
                String hex = Integer.toHexString(0xff & b);
                if (hex.length() == 1) {
                    hexString.append('0');
                }
                hexString.append(hex);
            }
            return hexString.toString();
        }

        public static void main(String[] args) {
            String signature = "signature";
            String publicKeyStr = "public key";
            String payloadStr = "{\"event\":\"PAYMENT_AUTHORIZED\",\"reference\":\"reference-id\",\"payment-id\":\"d76d1fcb-9a9e-489b-a71b-25304c2d8c5c\"}";

            try {
                String payloadHash = generateSHA256Hash(payloadStr);
                boolean isValid = verifyMessage(publicKeyStr, payloadHash, signature);
                System.out.println("The signature is " + (isValid ? "valid" : "invalid"));
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
    ```

=== "Python"

    ``` python
    import base64
    import hashlib

    from cryptography.exceptions import InvalidSignature
    from cryptography.hazmat.primitives import hashes
    from cryptography.hazmat.primitives import serialization
    from cryptography.hazmat.primitives.asymmetric import padding


    def generate_sha256_hash(string):
        return hashlib.sha256(string.encode('utf-8')).hexdigest()


    # Load the public key
    public_key_pem = b"""-----BEGIN PUBLIC KEY-----
    your-public-key
    -----END PUBLIC KEY-----"""
    public_key = serialization.load_pem_public_key(public_key_pem)

    # Decode the signature
    decoded_signature = base64.b64decode("the signature")

    # Hash the payload
    payload = '{"event":"PAYMENT_AUTHORIZED","reference":"reference-id","payment-id":"d76d1fcb-9a9e-489b-a71b-25304c2d8c5c"}'
    payload_hash = generate_sha256_hash(payload)

    # Verify the signature
    try:
        public_key.verify(
            decoded_signature,
            payload_hash.encode('utf-8'),
            padding.PKCS1v15(),
            hashes.SHA512()
        )
        print("The signature is valid.")
    except InvalidSignature:
        print("The signature is invalid.")
    ```


---

## **Webhook Delivery Confirmation**

To ensure reliable delivery of webhooks, we implement a retry mechanism and notification system.

### **Confirming Successful Reception**

A webhook is considered successfully delivered when the client's server responds with an HTTP status code in the `2XX` range. Specifically:

- Status codes `200-299` indicate successful reception.
- Any status code outside this range (e.g., `3XX`, `4XX`, `5XX`) is treated as a failed delivery and it will be considered as a non delivery webhook.

### **Retry Mechanism**

If the initial webhook delivery attempt fails, our system automatically initiates a series of retry attempts:

Retries are performed at increasing intervals:

- 5 tries
- With a backoff ratio of 1.1 over a 15 seconds interval
- Trigger rate, approximately, in seconds: 0, ~15, ~32, ~50, ~70

### **Notification Process for Persistent Failures**

If all retry attempts are exhausted without a successful delivery, our system triggers a notification process:

1. Notifications are sent to a predefined list of email addresses associated with the client's webhook configuration.
2. This email list is established during the initial webhook setup process.
3. The notification email includes:
    - Details of the failed webhook, like:
        - Timestamp
        - Payment and order reference
        - Event type