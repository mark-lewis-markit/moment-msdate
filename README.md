# moment-msdate [![Build Status](https://travis-ci.org/markitondemand/moment-msdate.svg?branch=master)](https://travis-ci.org/markitondemand/moment-msdate) [![npm version](https://badge.fury.io/js/moment-msdate.svg)](https://badge.fury.io/js/moment-msdate)

A [Moment.js](http://momentjs.com/) plugin for parsing OLE Automation dates. 

Visit [http://markitondemand.github.io/moment-msdate/](http://markitondemand.github.io/moment-msdate/) for more information and examples.

## About OLE Automation Dates

An OLE Automation date, or "MSDate" as we call it, is implemented as a floating-point number whose integral component is the number of days before or after midnight, 30 December 1899, and whose fractional component represents the time on that day divided by 24. For example, midnight, 31 December 1899 is represented by 1.0; 6 A.M., 1 January 1900 is represented by 2.25; midnight, 29 December 1899 is represented by -1.0; and 6 A.M., 29 December 1899 is represented by -1.25.

Read more [about OLE Automation on MSDN](http://msdn.microsoft.com/en-us/library/dt80be78(v=vs.71).aspx) (including [`DateTime.ToOADate`](http://msdn.microsoft.com/en-us/library/system.datetime.tooadate.aspx) and [`DateTime.FromOADate`](http://msdn.microsoft.com/en-us/library/system.datetime.fromoadate.aspx)).

## Usage

### toOADate()

Convert a `moment` to an OA date:

`moment().toOADate();`

This API returns a floating-point number (the OA date), so once the conversion has been made, you no longer have a `moment` object.

### fromOADate()

Convert an OA date to a `moment` (or to a JavaScript date):

`moment.fromOADate(41493)` returns `Wed Aug 07 2013 00:00:00 GMT-0600 (MDT)`

For exact date _and_ time (time is the value right of the decimal):

`moment.fromOADate(41493.706892280097000)` returns `Wed Aug 07 2013 16:57:55 GMT-0600 (MDT)`

By default moment.fromOADate() uses the server time as the offset to UTC a second argument can be provided that indicates the offset of the OA date to UTC in minutes.

`moment.fromOADate(42754.835023148145, 360)` returns `Fri Jan 20 2017 02:02:25 GMT+0000 (UTC)`

For Moment formatting:

```
//convert OA date into Moment (JavaScript date)
var momentDate = moment.fromOADate(41493.706892280097000);

//use Moment's awesomeness
var formattedDate = momentDate.format('MMM Do YY);

//formattedDate === "Aug 7th 13"
```

This could easily be chained together as:

`moment.fromOADate(41493.706892280097000).format('MMM Do YY); //Aug 7th 13`

**Note**: OLE Automation dates are unspecified, meaning they’re based on the local timezone by default.

### fromOADateWithZone()
Converts an OLE Automation date to a moment (baking in a timezone if one is supplied) and returns a UTC Moment object instance.

`moment.fromOADateWithZone('42754.835023148145', 'America/Denver');` returns `Fri Jan 20 2017 03:02:25 GMT+0000 (UTC)`

### toOADateWithZone()
Converts a moment (with timezone) to an OLE Automation date in UTC.

`moment('2017-01-19T20:02:26.000Z').toOADateWithZone()` returns `42754.835023148145`

## License

Copyright &copy; 2014 Markit On Demand, Inc.

The "moment-msdate" Moment.js plugin is licensed under the Apache License, Version 2.0.
