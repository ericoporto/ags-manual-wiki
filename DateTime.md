DateTime functions and properties
---------------------------------

[Now property](#DateTime.Now)\
[DayOfMonth property](#DateTime.DayOfMonth)\
[Hour property](#DateTime.Hour)\
[Minute property](#DateTime.Minute)\
[Month property](#DateTime.Month)\
[RawTime property](#DateTime.RawTime)\
[Second property](#DateTime.Second)\
[Year property](#DateTime.Year)

---

### Now property

*(Formerly known as GetTime, which is now obsolete)*

    readonly static DateTime* DateTime.Now;

Gets the current system time. You could use this for timing a loop, or
for effects like telling the player to go to bed, and so on.

A *DateTime* object is returned, which contains various properties that
you can use.

Note that the DateTime object that you get will not be kept up to date
with the current time; it will remain static with the time at which you
called DateTime.Now.

Example:

    DateTime *dt = DateTime.Now;
    Display("The date is: %02d/%02d/%04d", dt.DayOfMonth, dt.Month, dt.Year);
    Display("The time is: %02d:%02d:%02d", dt.Hour, dt.Minute, dt.Second);

will display the current date and time in 24-hour format

*See Also:* [DateTime.DayOfMonth](ags48#DateTime.DayOfMonth),
[DateTime.Hour](ags48#DateTime.Hour),
[DateTime.Minute](ags48#DateTime.Minute),
[DateTime.Month](ags48#DateTime.Month),
[DateTime.RawTime](ags48#DateTime.RawTime),
[DateTime.Second](ags48#DateTime.Second),
[DateTime.Year](ags48#DateTime.Year)

---

### DayOfMonth property

    readonly int DateTime.DayOfMonth;

Gets the day of the month represented by the DateTime object. This will
be from 1 to 31, representing the current day within the month.

Example: For an example, see [DateTime.Now](ags48#DateTime.Now).

*See Also:* [DateTime.Now](ags48#DateTime.Now)

---

### Hour property

    readonly int DateTime.Hour;

Gets the hour represented by the DateTime object. This will be from 0 to
23, representing the hour in 24-hour format.

Example: For an example, see [DateTime.Now](ags48#DateTime.Now).

*See Also:* [DateTime.Now](ags48#DateTime.Now)

---

### Minute property

    readonly int DateTime.Minute;

Gets the minute represented by the DateTime object. This will be from 0
to 59, representing the minute in 24-hour format.

Example: For an example, see [DateTime.Now](ags48#DateTime.Now).

*See Also:* [DateTime.Now](ags48#DateTime.Now)

---

### Month property

    readonly int DateTime.Month;

Gets the month represented by the DateTime object. This will be from 1
to 12, representing the month of the year.

Example: For an example, see [DateTime.Now](ags48#DateTime.Now).

*See Also:* [DateTime.Now](ags48#DateTime.Now)

---

### RawTime property

*(Formerly known as GetRawTime, which is now obsolete)*

    readonly int DateTime.RawTime;

This function returns the raw system time, as the number of seconds
since January 1970. While this value is not useful in itself, you can
use it to calculate time differences by getting the value at the start
of the game, for example, and then getting the value later on, and the
difference between the two is how much time has elapsed.

**NOTE:** Because this accesses the real-time clock on the users'
system, it is not a good idea to use this for long term timing tasks,
since if the user saves the game and then restores it later, the Time
value returned by this function will obviously include the difference
when they were not playing.

Example:

    DateTime *dt = DateTime.Now;
    int start_time = dt.RawTime;
    Wait(120);
    dt = DateTime.Now;
    Display("After the wait it is now %d seconds later.", dt.RawTime - start_time);

should display that 3 seconds have elapsed.

*See Also:* [DateTime.Now](ags48#DateTime.Now),
[SetTimer](ags54#SetTimer)

---

### Second property

    readonly int DateTime.Second;

Gets the second represented by the DateTime object. This will be from 0
to 59, representing the second.

Example: For an example, see [DateTime.Now](ags48#DateTime.Now).

*See Also:* [DateTime.Now](ags48#DateTime.Now)

---

### Year property

    readonly int DateTime.Year;

Gets the year represented by the DateTime object. This is the full year,
for example *2005*.

Example: For an example, see [DateTime.Now](ags48#DateTime.Now).

*See Also:* [DateTime.Now](ags48#DateTime.Now)