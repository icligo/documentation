# ProductDto

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**type** | **String** | Type of the product. | [optional] 
**name** | **String** | Name of the product. | [optional] 
**location** | **String** | Location of the product. | [optional] 
**duration** | **String** | Duration of the product/service. | [optional] 
**code** | **String** | Unique product code. | [optional] 
**transport** | **String** | Type of transport associated with the product, if applicable. | [optional] 
**checkin** | **Date** | Check-in date of the product, formatted as a string. | [optional] 
**checkout** | **Date** | Check-out date of the product, formatted as a string. | [optional] 
**_date** | **Date** | Date of the product activity or service, formatted as a string. | [optional] 
**price** | **BigDecimal** | Price of the product. | [optional] 
**detail** | [**DetailDto**](DetailDto.md) |  | [optional] 

<a name="TypeEnum"></a>
## Enum: TypeEnum

* `BOOKING` (value: `"BOOKING"`)
* `SUBSCRIPTION` (value: `"SUBSCRIPTION"`)
* `GIFT` (value: `"GIFT"`)
* `EVENT` (value: `"EVENT"`)
* `SERVICE` (value: `"SERVICE"`)
* `ACCOMMODATION` (value: `"ACCOMMODATION"`)
* `FLIGHT` (value: `"FLIGHT"`)
* `PACKAGE` (value: `"PACKAGE"`)
* `INSURANCE` (value: `"INSURANCE"`)
* `CRUISE` (value: `"CRUISE"`)
* `ACTIVITY` (value: `"ACTIVITY"`)
* `TRANSFER` (value: `"TRANSFER"`)


<a name="TransportEnum"></a>
## Enum: TransportEnum

* `CAR` (value: `"CAR"`)
* `BUS` (value: `"BUS"`)
* `TRAIN` (value: `"TRAIN"`)

