
# TestPlan for GET /carsharing/cars

Usecase | Test data |Expected result|Actual result|Description|automated (y/n)|comments
---------|----------|---------
 Invalid language or language format is specified in the input  | language="FRAccc" | error 001- Invalid language.||
User does not have the needed rights to shoot the API but he tries to do so||error 002 You are missing the rights to perform this action.
User specifies loaction and start dateTime but there are no cars available.||error 003 No cars available near the selected location at the selected time.
User specifies city which does not exist in the selected country|error 004 Invalid city. |
Zipcode is wrongly specified or does not exist in the selected country|error 005 Invalid zipcode. |
Country is wrongly specified.|error 006 Specified country does not exist. |
Address is wrongly specified or does not exist in the selected town|error 007 Invalid address. |
User specifies carsharing station which is not registered for carsharing (all valid stations should be listed in the enum field in stationName query parameter)|error 008 Invalid carsharing station. |
User specifies date in wrong format|error 009 Invalid date format. |
User specifies time in wrong format|error 010 Invalid time format. |
User specifies dateTime in wrong format|error 011 Invalid DateTime format.|error 014 The date and the time can not be in the past.
Invalid currency format or currency that does not exist is specified in the input  | currency="EURO" | error 016 Invalid currency.||
User specifies country+startDateTime| F
User specifies country + city+startDateTime|F
User specifies country+zipcode+startDateTime|F
User specifies country+city+zipcode+startDateTime|T
User specifies country+city+zipcode+full address+startDateTime|T
User specifies country+station+startDateTime|T
User specifies country+city+station+startDateTime|T
User specifies country+city+zipcode+full address+station+startDateTime|T-
eturns cars available at the station
User specifies userXcordinate+userYcoordinate+startDateTime|T
User specifies userXcordinate+startDateTime|F
User specifies userYcoordinate+startDateTime|F
User specifies country+city+zipcode+full address|F datetime missing
User specifies country+city+zipcode+full address+startDate|F time missing
User specifies country+city+zipcode+full address+startTime|F date missing
User specifies country+city+zipcode+full address+startDate+startTime|F datetime missing
User specifies startDate+startTime|F location missing

