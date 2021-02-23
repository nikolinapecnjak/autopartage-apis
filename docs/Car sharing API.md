# Carsharing API

Carsharing is is a model of car rental where people rent cars for short periods of time, often by the hour or by minutes. There are also carsharing models which enable to rent a car for couple of days.
This set of APIs covers different functionalities such as retrieving available cars, making a carsharing reservation,
reviewing carsharing reservation details...
For the moment following APIs are available:
- Retrieve cars available for the carsharing
This set of APIs is generic and can be used for different business models of carsharing services.
## General Data Model


## GET /carsharing/cars

This API returns the cars available for the carsharing service according to the requester matching input parameters.

### Input
All the query parameters are case insensitive.
In order to specify the request it is needed at least to uniquely specify the location and the start date/dateTime.

Following table gives the visibility of correct input combinations for the Location listed with the priorities:


Fields combination | Priority |Description
---------|----------|---------
 country + zipcode + city | 4 |defines the city where the car is searched
 country+ zipcode + city + fullAddress | 3|defines the address around which the car is searched
 country + stationName | 2 | defines the carsharing station
 userXCoordinate + userYCoordinate | 1 |defines user location 

In case if more combinations are specified in the same request, the order of priority will be applied as listed in the table above and all other combinations are ignored.
If at least one of the above combinations is not selected, the error is returned.

Following table gives the visibility of correct input combinations for the Time period of carsharing rent :

Fields combination | Priority | Description
---------|----------|---------
 startDateTime (or startDate+startTime) | 3 | Used for usecases where car is booked instantly at the time of the search or when the user wants to reserve the car at specific date and time.
startDateTime (or startDate+startTime) + endDateTime (or endDate+endTime) | 1 | Used for usecases when car can be rented for specific number of days and the end date and time needs to be selected in advance.

 The allowed input combinations depend on the business model of the company. Some input combinations wont be applicable for some models and they will be ignored, but the API gives the possibility since it is generic.

 All other input parameters are optional.
### Output
This api returns an array of Car objects matching the input parameters.
Car object represents the available for the rent through the carsharing service. Except required parameters it is mandatory to return one of the prices. It depends on the business model which type of pricing is used and which parameter should be returned. It can be specified in the request 'fields' parameters which parameters should be returned. It is possible to have daily pricing, hourly pricing, pricing per minute and pricing per kilometer.
### Error Codes


### Example

```json
{
  "id": "string",
  "location": {
    "id": "string",
    "country": "France",
    "city": "Nice",
    "zipCode": 6100,
    "fullAddress": "1er Albert Premier",
    "stationName": "Gare de Nice-Ville",
    "description": "train station",
    "isAirport": true,
    "kmDistanceFromSelectedLocation": 1.5,
    "xCoordinate": 43.575847,
    "yCoordinate": 7.120708
  },
  "carBrand": "BMW",
  "carModel": "BMW 5",
  "fuelOrBatteryLevel": "70%",
  "numberOfSeats": "4",
  "description": "Equiped with climatisation and snow tires. ",
  "fuelType": "diesel",
  "fuelCardIncluded": true,
  "airConditioning": true,
  "gps": true,
  "snowTires": true,
  "speedRegulator": true,
  "halfAutonomyLevel": true,
  "kilometersLeft": 1500,
  "carClass": "S",
  "platesNumber": "FW228GZ",
  "carYear": 2017,
  "kilometersPassed": 50000,
  "kilometerPrice": "1",
  "hourPrice": "10",
  "minutePrice": "0.50",
  "dayPrice": "100",
  "transmission": "manual",
  "energy": "thermal",
  "carType": "",
  "currencyCode": "EUR"
}
```