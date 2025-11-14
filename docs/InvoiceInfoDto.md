# InvoiceInfoDto

## Properties

| Name            | Type                            | Description                                                                   | Notes |
|-----------------|---------------------------------|-------------------------------------------------------------------------------|-------|
| **requested**          | **Boolean**                      | Flag indicating whether billing data has been requested.                              | required     |
| **name** | **String**                        | Name on the billing information.                              | Required if `requested = true`     |
| **documentNumber** | **String**                      | Billing document number.                                                   | Required if `requested = true`     |
| **email**      | **String** | Billing email address. | Required if `requested = true`     |
| **address**      | **String** | Billing address. | Required if `requested = true`     |
| **country**      | **String** | Billing address ISO 3166-1 alpha-2 country code. | Required if `requested = true`     |
| **city**      | **String** | City of the billing address. | Required if `requested = true`     |
| **postCode**      | **String** | Postal code of the billing address. | Required if `requested = true`     |
