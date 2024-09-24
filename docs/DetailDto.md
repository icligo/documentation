# DetailDto

## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**night** | **Number** | Number of nights for the stay. | [optional] 
**roomType** | **String** | Room type for accommodation. | [optional] 
**regime** | **String** | Accommodation regime. | [optional] 
**flightNumber** | **String** | Flight number for associated transportation. | [optional] 
**departure** | **Date** | Departure date for the transportation, formatted as a string. | [optional] 
**arrival** | **Date** | Arrival date for the transportation, formatted as a string. | [optional] 
**departureTime** | **String** | Departure time for the flight or transportation. | [optional] 
**arrivalTime** | **String** | Arrival time for the flight or transportation. | [optional] 
**departureAirport** | **String** | Departure airport code. | [optional] 
**arrivalAirport** | **String** | Arrival airport code. | [optional] 
**departureCity** | **String** | City of departure. | [optional] 
**arrivalCity** | **String** | City of arrival. | [optional] 
**departureCountry** | **String** | Country of departure. | [optional] 
**arrivalCountry** | **String** | Country of arrival. | [optional] 
**baggage** | **String** | Baggage details for the transportation. | [optional] 
**duration** | **String** | Duration of the transportation or stay. | [optional] 
**provider** | **String** | Service provider for the product or service. | [optional] 
**reception** | **String** | Reception details. | [optional] 
**receptionTime** | **Date** | Time of reception at the destination. | [optional] 
**destinationTime** | **Date** | Time of arrival at the destination. | [optional] 
**destination** | **String** | Destination details. | [optional] 
**circuit** | [**[CircuitDto]**](CircuitDto.md) | Details of the circuit, if applicable. | [optional] 
**stopovers** | [**[StopoversDto]**](StopoversDto.md) | Details of stopovers during transportation, if applicable. | [optional] 

<a name="RoomTypeEnum"></a>
## Enum: RoomTypeEnum

* `inside` (value: `"Inside"`)
* `oceanview` (value: `"Oceanview"`)
* `balcony` (value: `"Balcony"`)
* `suite` (value: `"Suite"`)

