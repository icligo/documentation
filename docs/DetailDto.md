# DetailDto

## Properties

| Name                 | Type                                | Description                                                   | Notes      |
|----------------------|-------------------------------------|---------------------------------------------------------------|------------|
| **night**            | **Integer**                         | Number of nights for the stay.                                | [optional] |
| **roomType**         | [**RoomTypeEnum**](RoomTypeEnum.md) | Room type for accommodation.                                  | [optional] |
| **regime**           | **String**                          | Accommodation regime.                                         | [optional] |
| **flightNumber**     | **String**                          | Flight number for associated transportation.                  | [optional] |
| **departure**        | **Date**                            | Departure date for the transportation, formatted as a string. | [optional] |
| **arrival**          | **Date**                            | Arrival date for the transportation, formatted as a string.   | [optional] |
| **departureTime**    | **String**                          | Departure time for the flight or transportation.              | [optional] |
| **arrivalTime**      | **String**                          | Arrival time for the flight or transportation.                | [optional] |
| **departureAirport** | **String**                          | Departure airport code.                                       | [optional] |
| **arrivalAirport**   | **String**                          | Arrival airport code.                                         | [optional] |
| **departureCity**    | **String**                          | City of departure.                                            | [optional] |
| **arrivalCity**      | **String**                          | City of arrival.                                              | [optional] |
| **departureCountry** | **String**                          | Country of departure.                                         | [optional] |
| **arrivalCountry**   | **String**                          | Country of arrival.                                           | [optional] |
| **baggage**          | **String**                          | Baggage details for the transportation.                       | [optional] |
| **duration**         | **String**                          | Duration of the transportation or stay.                       | [optional] |
| **provider**         | **String**                          | Service provider for the product or service.                  | [optional] |
| **reception**        | **String**                          | Reception details.                                            | [optional] |
| **receptionTime**    | **Date**                            | Time of reception at the destination.                         | [optional] |
| **destinationTime**  | **Date**                            | Time of arrival at the destination.                           | [optional] |
| **destination**      | **String**                          | Destination details.                                          | [optional] |
| **circuit**          | [**CircuitDto**](CircuitDto.md)     | Details of the circuit, if applicable.                        | [optional] |
| **stopovers**        | [**StopoversDto**](StopoversDto.md) | Details of stopovers during transportation, if applicable.    | [optional] |

## Example

```json
{
  "night": 3,
  "roomType": "Suite",
  "regime": "Half board",
  "flightNumber": "FL123",
  "departure": "2024-09-24T16:46:42.411Z",
  "arrival": "2024-09-24T16:46:42.411Z",
  "departureTime": "2024-09-24T16:46:42.411Z",
  "arrivalTime": "string",
  "departureAirport": "JFK",
  "arrivalAirport": "LHR",
  "departureCity": "New York",
  "arrivalCity": "London",
  "departureCountry": "US",
  "arrivalCountry": "UK",
  "baggage": "string",
  "duration": "string",
  "provider": "Airline XYZ",
  "reception": "string",
  "receptionTime": "2024-09-24T16:46:42.411Z",
  "destinationTime": "2024-09-24T16:46:42.411Z",
  "destination": "string",
  "circuit": [
    {
      "checkin": "2024-09-24T16:46:42.411Z",
      "checkout": "2024-09-24T16:46:42.411Z",
      "location": "string"
    }
  ],
  "stopovers": [
    {
      "departure": "2024-09-24T16:46:42.411Z",
      "arrival": "2024-09-24T16:46:42.411Z",
      "departureTime": "2024-09-24T16:46:42.411Z",
      "arrivalTime": "2024-09-24T16:46:42.411Z",
      "departureAirport": "string",
      "arrivalAirport": "string",
      "departureCity": "string",
      "arrivalCity": "string",
      "departureCountry": "string",
      "arrivalCountry": "string",
      "duration": "2H"
    }
  ]
}
```

