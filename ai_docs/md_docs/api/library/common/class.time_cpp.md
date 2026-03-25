# Unigine::Time Class (CPP)

**Header:** #include <UnigineTimer.h>


This class is used to get the current system time and convert it to various untis.


> **Notice:** **This class has no implementation in Engine's C# API** as there are other options available:
>
>
> **[Stopwatch.GetTimestamp()](https://learn.microsoft.com/en-us/dotnet/api/system.diagnostics.stopwatch.gettimestamp?view=net-8.0#system-diagnostics-stopwatch-gettimestamp)** method (from the standard **System.Diagnostics** module) is the most accurate and closest to wall-clock time. It returns seconds as a double precision, allowing operation with microseconds/nanoseconds. It ignores spikes and freezes. Can be used for any application independent time calculations.
>
>
> In case you don't need time accuracy that high, you can simply use the standard and convenient **[DateTime.Now](https://learn.microsoft.com/en-us/dotnet/api/system.datetime.now?view=net-8.0)** property.


## Timer Class

### Members

---

## static double microsecondsToNanoseconds ( long long microseconds )

Converts microseconds to nanoseconds.
### Arguments

- *long long* **microseconds** - Microseconds.

### Return value

Nanoseconds.
## static double microsecondsToMilliseconds ( long long microseconds )

Converts microseconds to milliseconds.
### Arguments

- *long long* **microseconds** - Microseconds.

### Return value

Milliseconds.
## static double microsecondsToSeconds ( long long microseconds )

Converts microseconds to seconds.
### Arguments

- *long long* **microseconds** - Microseconds.

### Return value

Seconds.
## static double millisecondsToNanoseconds ( double milliseconds )

Converts milliseconds to nanoseconds.
### Arguments

- *double* **milliseconds** - Milliseconds.

### Return value

Nanoseconds.
## static double millisecondsToMicroseconds ( double milliseconds )

Converts milliseconds to microseconds.
### Arguments

- *double* **milliseconds** - Milliseconds.

### Return value

Microseconds.
## static double millisecondsToSeconds ( double milliseconds )

Converts milliseconds to seconds.
### Arguments

- *double* **milliseconds** - Milliseconds.

### Return value

Seconds.
## static double secondsToNanoseconds ( double seconds )

Converts seconds to nanoseconds.
### Arguments

- *double* **seconds** - Seconds.

### Return value

Nanoseconds.
## static double secondsToMicroseconds ( double seconds )

Converts seconds to microseconds.
### Arguments

- *double* **seconds** - Seconds.

### Return value

Microseconds.
## static double secondsToMilliseconds ( double seconds )

Converts seconds to milliseconds.
### Arguments

- *double* **seconds** - Seconds.

### Return value

Milliseconds.
## static double hertzToNanoseconds ( double hertz )

Converts frequency given in hertz to nanoseconds.
### Arguments

- *double* **hertz** - Hertz.

### Return value

Nanoseconds.
## static double hertzToMicroseconds ( double hertz )

Converts frequency given in hertz to microseconds.
### Arguments

- *double* **hertz** - Hertz.

### Return value

Microseconds.
## static double hertzToMilliseconds ( double hertz )

Converts frequency given in hertz to milliseconds.
### Arguments

- *double* **hertz** - Hertz.

### Return value

Milliseconds.
## static double hertzToSeconds ( double hertz )

Converts frequency given in hertz to seconds.
### Arguments

- *double* **hertz** - Hertz.

### Return value

Seconds.
## static long long getClock ( )

Returns CPU clock counter.
### Return value

CPU clock counter.
## static long long get ( )

Returns time in microseconds.
### Return value

Time in microseconds.
## static double getSeconds ( )

Returns time in seconds.
### Return value

Time in seconds.
## static double getMilliseconds ( )

Returns time in milliseconds.
### Return value

Time in milliseconds.
