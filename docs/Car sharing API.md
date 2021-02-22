# Carsharing API

Carsharing is is a model of car rental where people rent cars for short periods of time, often by the hour or by minutes. There are also carsharing models which enable to rent a car for couple of days.
This set of APIs covers different functionalities such as retrieving available cars, making a carsharing reservation,
reviewing carsharing reservation details...
For the moment following APIs are available:
- Retrieve cars available for the carsharing
This set of APIs is generic and can be used for different business models of carsharing services.
## General Data Model
[Data Model]()

## GET /carsharing/cars
[](assets/images/SearchCars-UseCases.png)
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
This api returns the array of Car objects matching the input parameters.
### Error Codes

### Example