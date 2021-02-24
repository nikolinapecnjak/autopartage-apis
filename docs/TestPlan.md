
# TestPlan for GET /carsharing/cars

Usecase | Test data |Expected result|Actual result|Description|automated (y/n)|comments
---------|----------|---------
Invalid language or language format is specified in the input  | language="FRAccc" | error 001- Invalid language.|
User does not have the needed rights to shoot the API but he tries to do so||error 002 You are missing the rights to perform this action.
User specifies loaction and start dateTime but there are no cars available.|country="France"&stationName="Nice Airport"&startDateTime="2021-07-21T17:32:28Z",|error 003 No cars available near the selected location at the selected time.
User specifies city which does not exist in the selected country| country=  "France" &city ="Niceaa"  Nice|error 004 Invalid city. |
Zipcode is wrongly specified or does not exist in the selected country|country="France" &city ="Nice"&zipCode="610000"|error 005 Invalid zipcode. |
Country is wrongly specified.|country="Franceaaa"|error 006 Specified country does not exist. |
Address is wrongly specified or does not exist in the selected town|country="France" city ="Nice" &zipCode="6100"&fullAddress="1er Albert Premieraaa"|error 007 
Invalid address. |
User specifies carsharing station which is not registered for carsharing (all valid stations should be listed in the enum field in stationName query parameter)|country="France"&stationName="Nonexisting station"&startDateTime="2021-07-21T17:32:28Z"|error 008 Invalid carsharing station. |
User specifies date in wrong format|country="France"&city ="Nice"&startDate="20211-07-21"|error 009 Invalid date format.|
User specifies time in wrong format|country="France"&city="Nice"&startDate="2021-07-21"&startTime="177:32:28|error 010 Invalid time format. |
User specifies dateTime in wrong format|country="France"&stationName="Nice Airport"&startDateTime="2021:07-21T17:32:28Z"|error 011 Invalid DateTime format.
User specifies the date or time in the past|country="France"&stationName="Nice Airport"&startDateTime="2019-07-21T17:32:28Z"|error 014 The date and the time can not be in the past.
Invalid currency format or currency that does not exist is specified in the input  | currency="EURO" | error 016 Invalid currency.||
User specifies country+startDateTime|country="France"&startDateTime="2021-07-21T17:32:28Z"|  017-Required parameter missing.Please specify at least the city or the stationName together with the country.
User specifies country + city+startDateTime|country="France"&city="Nice"&startDateTime="2021-07-21T17:32:28Z"|012 -Required parameter missing.Please specify the location
User specifies country+zipcode+startDateTime|country="France"&zipCode="6100"&startDateTime="2021-07-21T17:32:28Z"|012 -Required parameter missing.Please specify the location.
User specifies country+city+zipcode+startDateTime|country="France"&city="Nice"&zipCode="6100"&startDateTime="2021-07-21T17:32:28Z"|200 OK
User specifies country+city+zipcode+full address+startDateTime|country="France"&city="Nice"&zipCode="6100"&fullAddress="1er Albert Premier"&startDateTime="2021-07-21T17:32:28Z"|200 OK
User specifies country+station+startDateTime|country="France"&stationName="Gare de Nice-Ville"&startDateTime="2021-07-21T17:32:28Z"|200 OK
User specifies country+city+station+startDateTime|country="France"&city ="Nice"&stationName="Gare de Nice-Ville"&startDateTime="2021-07-21T17:32:28Z"|200 ok|Cars available at the station are returned since station has higher priority than city.
User specifies country+city+zipcode+full address+station+startDateTime|country="France"&city ="Nice"&zipCode="6100"&stationName="Gare de Nice-Ville"&fullAddress="1er Albert Premier"&startDateTime="2021-07-21T17:32:28Z"|200 OK|Returns cars available at the station since station ih higher priority than the address
User specifies userXcordinate+userYcoordinate+startDateTime|userXCoordinate="43.575847"&userYCoordinate="7.120708"&startDateTime="2021-07-21T17:32:28Z"|200 OK|Returns the cars near the user location (radius is not specified so the default value is taken)
User specifies userXcordinate+startDateTime|userXCoordinate="43.575847"&startDateTime="2021-07-21T17:32:28Z"|012 -Required parameter missing.Please specify the location.
User specifies userYcoordinate+startDateTime|userYCoordinate="7.120708"&startDateTime="2021-07-21T17:32:28Z"|012 -Required parameter missing.Please specify the location.
User specifies country+city+zipcode+full address|country="France" &city ="Nice" &zipCode="6100"&fullAddress="1er Albert Premier"|013 -Required parameter missing.Please specify the date and the time.
User specifies country+city+zipcode+full address+startDate|country="France" &city ="Nice" &zipCode="6100"&fullAddress="1er Albert Premier"&startTime="17:32:28|013 -Required parameter missing.Please specify the date and the time.
User specifies country+city+zipcode+full address+startTime|country="France" &city ="Nice" &zipCode="6100"&fullAddress="1er Albert Premier"&startTime="17:32:28|013 -Required parameter missing.Please specify the date and the time.
User specifies country+city+zipcode+full address+startDate+startTime|country="France" &city ="Nice" &zipCode="6100"&fullAddress="1er Albert Premier"&startDate="2021-07-21"&startTime="17:32:28|200 OK
User specifies startDate+startTime|startDate="2021-07-21"&startTime="17:32:28|012 -Required parameter missing.Please specify the location.
  User specifies startDateTime|startDateTime="2021-07-21T17:32:28Z"|012 -Required parameter missing.Please specify the location.
  User specifies invalid coordinates|userXCoordinate="43)-5.575847"&userYCoordinate="7.120708"&startDateTime="2021-07-21T17:32:28Z"|015 -Invalid user coordinates.

