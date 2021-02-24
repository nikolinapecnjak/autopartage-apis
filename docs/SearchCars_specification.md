# Carsharing API

Carsharing is is a model of car rental where people can rent cars for a short period of time, often measured by the hour or by minutes. There are also carsharing models which enable to rent a car for several days.
This set of APIs covers different functionalities such as retrieving available cars, making a carsharing reservation,
reviewing carsharing reservation details...
For the moment following APIs are available:
- Retrieve cars available for the carsharing
This set of APIs is generic and can be used for different business models of carsharing services.
## General Data Model
General Data Model can be found by name Data Model in images folder.

## GET /carsharing/cars

Use Case UML Model can be found by name SearchCars-Useses in images folder.

This API returns the cars available for the carsharing service according to the requester matching input parameters.

### Input
All the query parameters are case insensitive.
In order to specify the request it is needed at least to uniquely specify the start location and the start date/dateTime.
Depending on the business model of the carsharing service,endDateTime (or endDate+endTime) might also be required.

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
 startDateTime (or startDate+startTime) | 2 | Used for usecases where car is booked instantly at the time of the search or when the user wants to reserve the car at specific date and time.
startDateTime (or startDate+startTime) + endDateTime (or endDate+endTime) | 1 | Used for usecases when car can be rented for specific number of days and the end date and time needs to be selected in advance.

 The allowed input combinations depend on the business model of the company. Some input combinations wont be applicable for some models and they will be ignored, but the API gives the possibility since it is generic.

 All other input parameters are optional.
### Output
This api returns an array of Car objects matching the input parameters.
Car object represents the available for the rent through the carsharing service. Except required parameters it is mandatory to return one of the prices. It depends on the business model which type of pricing is used and which parameter should be returned. It can be specified in the request 'fields' parameters which parameters should be returned. It is possible to have daily pricing, hourly pricing, pricing per minute and pricing per kilometer.
### Error Codes
If any of the optional input values fields is filled wrongly, that parameter is ignored or default value is applied if it exists.

Error Code | Error Text | HTTP Code |DESCRIPTION
---------|----------|---------
001|Invalid language.|403|Wrong language format is specified or specified language does not exist
 002 |You are missing the rights to perform this action. | 403|User has no rights to shoot the API.|
 003 | No cars available near the selected location at the selected time. | 204||
 004 | Invalid city.| 400 |  City is wrongly specified or does not exist in the selected country| 
   005 |Invalid zipcode. | 400 |  Zipcode is wrongly specified or does not exist in the selected country| 
   006 |Specified country does not exist.| 400 | Country is wrongly specified.| 
   007 | Invalid address.| 400 |  Address is wrongly specified or does not exist in the selected town| 
   008 | Invalid carsharing station. | 400 |Selected station does not exist.  | 
  009 |Invalid date format.| 400 |startDate/endDate is wrongly specified | 
 010 | Invalid time format. | 400 | startTime/endTime/startDateTime or endDateTime is wrongly specified|
 011 | Invalid DateTime format. | 400 | startDateTime or endDateTime is wrongly specified| 
 012 |Required parameter missing.Please specify the location. | 400 |One of the required parameters needed to specify the location is missing | 
 013 |Required parameter missing.Please specify the date and the time.  | 400 | One of the required parameters needed to specify the date or time is missing.| 
 014 |The date and the time can not be in the past.  | 400 | Date or time are specified in the past.| 
 015 |Invalid user coordinates. | 400 | User x and y coordinate are not following the format.| 
016|Invalid currency.|403|Wrong currency format is specified or specified currency does not exist|
017|Required parameter missing.Please specify at least the city or the stationName together with the country.|403|When only country is specified as a location.|


### Response Example

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