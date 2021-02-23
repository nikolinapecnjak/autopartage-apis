
# TestPlan for GET /carsharing/cars

Usecase | Test data | Description |Expected result|Actual result|automated (y/n)|comments
---------|----------|---------
 Some of the optional parameters is wrongly specified | language="FRAccc" | Default value is provided ih there is one,otherwise the parameter is ignored.  | |laguage:"FRA"
 City is wrongly specified or does not exist in the selected country | B2 | Invalid city.| |
  Zipcode is wrongly specified or does not exist in the selected country | B2 | Invalid zipcode.| |
   Country is wrongly specified| B2 | Country does not exist.| |
   Address is wrongly specified or does not exist in the selected town | B2 | Invalid address| |
   Selected station does not exist. | B2 | Invalid carsharing station.| |
 startDate/endDate is wrongly specified | B3 | Invalid date format.| |
 Some of the required | B3 | Invalid date format.| |
 startTime/endTime/startDateTime or endDateTime is wrongly specified | B3 | Invalid time format.| |
startDateTime or endDateTime is wrongly specified | B3 | Invalid DateTime format.| |
One of the required parameters needed to specify the location is missing | B3 | Required parameter missing.Please specify location| |
One of the required parameters needed to specify the date or time is missing | B3 | Required parameter missing.Please specify the date and the time.| |

