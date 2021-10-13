# format-time-or-data-golang

[Format a time or date [complete guide] · YourBasic Go.pdf](https://github.com/fenriz07/format-time-or-data-golang/files/7340777/Format.a.time.or.date.complete.guide.YourBasic.Go.pdf)


https://yourbasic.org/golang/format-parse-string-time-date-example/

GOLANG Format a time or date

Basic example

Go doesn’t use yyyy-mm-dd layout to format a time. Instead, you format a special layout parameter

Mon Jan 2 15:04:05 MST 2006

the same way as the time or date should be formatted. (This date is easier to remember when written as 01/02 03:04:05PM ‘06 -0700.)

const (
    layoutISO = "2006-01-02"
    layoutUS  = "January 2, 2006"
)
date := "1999-12-31"
t, _ := time.Parse(layoutISO, date)
fmt.Println(t)                  // 1999-12-31 00:00:00 +0000 UTC
fmt.Println(t.Format(layoutUS)) // December 31, 1999


The function

    time.Parse parses a date string, and
    Format formats a time.Time.

They have the following signatures:

func Parse(layout, value string) (Time, error)
func (t Time) Format(layout string) string

Standard time and date formats
Go layout 	Note
January 2, 2006 	Date
01/02/06 	
Jan-02-06 	
15:04:05 	Time
3:04:05 PM 	
Jan _2 15:04:05 	Timestamp
Jan _2 15:04:05.000000 	with microseconds
2006-01-02T15:04:05-0700 	ISO 8601 (RFC 3339)
2006-01-02 	
15:04:05 	
02 Jan 06 15:04 MST 	RFC 822
02 Jan 06 15:04 -0700 	with numeric zone
Mon, 02 Jan 2006 15:04:05 MST 	RFC 1123
Mon, 02 Jan 2006 15:04:05 -0700 	with numeric zone

The following predefined date and timestamp format constants are also available.

ANSIC       = "Mon Jan _2 15:04:05 2006"
UnixDate    = "Mon Jan _2 15:04:05 MST 2006"
RubyDate    = "Mon Jan 02 15:04:05 -0700 2006"
RFC822      = "02 Jan 06 15:04 MST"
RFC822Z     = "02 Jan 06 15:04 -0700"
RFC850      = "Monday, 02-Jan-06 15:04:05 MST"
RFC1123     = "Mon, 02 Jan 2006 15:04:05 MST"
RFC1123Z    = "Mon, 02 Jan 2006 15:04:05 -0700"
RFC3339     = "2006-01-02T15:04:05Z07:00"
RFC3339Nano = "2006-01-02T15:04:05.999999999Z07:00"
Kitchen     = "3:04PM"
// Handy time stamps.
Stamp      = "Jan _2 15:04:05"
StampMilli = "Jan _2 15:04:05.000"
StampMicro = "Jan _2 15:04:05.000000"
StampNano  = "Jan _2 15:04:05.000000000"

Layout options
Type 	Options
Year 	06   2006
Month 	01   1   Jan   January
Day 	02   2   _2   (width two, right justified)
Weekday 	Mon   Monday
Hours 	03   3   15
Minutes 	04   4
Seconds 	05   5
ms μs ns 	.000   .000000   .000000000
ms μs ns 	.999   .999999   .999999999   (trailing zeros removed)
am/pm 	PM   pm
Timezone 	MST
Offset 	-0700   -07   -07:00   Z0700   Z07:00
Corner cases

It’s not possible to specify that an hour should be rendered without a leading zero in a 24-hour time format.

It’s not possible to specify midnight as 24:00 instead of 00:00. A typical usage for this would be giving opening hours ending at midnight, such as 07:00-24:00.

It’s not possible to specify a time containing a leap second: 23:59:60. In fact, the time package assumes a Gregorian calendar without leap seconds.

