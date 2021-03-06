# Time

Time is an abstraction of dates and times. Time is stored internally as the
number of seconds with fraction since the *Epoch*, January 1, 1970 00:00 UTC.
Also see the library module Date. The Time class treats GMT (Greenwich Mean
Time) and UTC (Coordinated Universal Time) as equivalent. GMT is the older way
of referring to these baseline times but persists in the names of calls on
POSIX systems.

All times may have fraction. Be aware of this fact when comparing times with
each other -- times that are apparently equal when displayed may be different
when compared.

Since Ruby 1.9.2, Time implementation uses a signed 63 bit integer, Bignum or
Rational. The integer is a number of nanoseconds since the *Epoch* which can
represent 1823-11-12 to 2116-02-20. When Bignum or Rational is used (before
1823, after 2116, under nanosecond), Time works slower as when integer is
used.

# Examples

All of these examples were done using the EST timezone which is GMT-5.

## Creating a new Time instance

You can create a new instance of Time with Time::new. This will use the
current system time. Time::now is an alias for this. You can also pass parts
of the time to Time::new such as year, month, minute, etc. When you want to
construct a time this way you must pass at least a year. If you pass the year
with nothing else time will default to January 1 of that year at 00:00:00 with
the current system timezone. Here are some examples:

    Time.new(2002)         #=> 2002-01-01 00:00:00 -0500
    Time.new(2002, 10)     #=> 2002-10-01 00:00:00 -0500
    Time.new(2002, 10, 31) #=> 2002-10-31 00:00:00 -0500
    Time.new(2002, 10, 31, 2, 2, 2, "+02:00") #=> 2002-10-31 02:02:02 +0200

You can also use #gm, #local and #utc to infer GMT, local and UTC timezones
instead of using the current system setting.

You can also create a new time using Time::at which takes the number of
seconds (or fraction of seconds) since the [Unix
Epoch](http://en.wikipedia.org/wiki/Unix_time).

    Time.at(628232400) #=> 1989-11-28 00:00:00 -0500

## Working with an instance of Time

Once you have an instance of Time there is a multitude of things you can do
with it. Below are some examples. For all of the following examples, we will
work on the assumption that you have done the following:

    t = Time.new(1993, 02, 24, 12, 0, 0, "+09:00")

Was that a monday?

    t.monday? #=> false

What year was that again?

    t.year #=> 1993

Was it daylight savings at the time?

    t.dst? #=> false

What's the day a year later?

    t + (60*60*24*365) #=> 1994-02-24 12:00:00 +0900

How many seconds was that since the Unix Epoch?

    t.to_i #=> 730522800

You can also do standard functions like compare two times.

    t1 = Time.new(2010)
    t2 = Time.new(2011)

    t1 == t2 #=> false
    t1 == t1 #=> true
    t1 <  t2 #=> true
    t1 >  t2 #=> false

    Time.new(2010,10,31).between?(t1, t2) #=> true

[Time Reference](https://ruby-doc.org/core-2.5.0/Time.html)
