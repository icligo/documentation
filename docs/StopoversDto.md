# StopoversDto

## Properties

| Name                 | Type       | Description                                                                  | Notes      |
|----------------------|------------|------------------------------------------------------------------------------|------------|
| **departure**        | **Date**   | The date and time when the departure occurs.                                 | [optional] |
| **arrival**          | **Date**   | The date and time when the arrival occurs.                                   | [optional] |
| **departureTime**    | **String** | The time of departure in a specified format (e.g., HH:MM).                   | [optional] |
| **arrivalTime**      | **String** | The time of arrival in a specified format (e.g., HH:MM).                     | [optional] |
| **departureAirport** | **String** | The airport from which the journey departs.                                  | [optional] |
| **arrivalAirport**   | **String** | The airport at which the journey arrives.                                    | [optional] |
| **departureCity**    | **String** | The city from which the journey departs.                                     | [optional] |
| **arrivalCity**      | **String** | The city at which the journey arrives.                                       | [optional] |
| **departureCountry** | **String** | The country from which the journey departs.                                  | [optional] |
| **arrivalCountry**   | **String** | The country at which the journey arrives.                                    | [optional] |
| **duration**         | **String** | The total duration of the journey, typically expressed in hours and minutes. | [optional] |

## Example

```json
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
```

