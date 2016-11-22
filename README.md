# make-unix-timestamp-c
## Purpose
Provides a simple C function that takes datetime elements (e.g. `seconds`, `minutes`, `hours`, `date`, `month` and `year`) and returns a single integer representing the number of seconds elapsed since the UNIX epoch (1/1/1970).

```c
uint32_t
unix_time_in_seconds( uint8_t sec, uint8_t min, uint8_t hrs, uint8_t day, uint8_t mon, uint16_t year );
```

This is a fairly common problem I've encountered, as many off-the-shelf RTC integrated circuits seem to only provide datetime output as the individual datetime elements, each accessed by a separate register.  However, it is easier to do most datetime/timer/looper logic operations using a well ordered set such as the integers, for which purpose a UNIX timestamp is ideal.

## Usage
You can build and run the example application simply:

```bash
make && ./example
```

The example app simply takes the datetime 6:53:16Z Nov 22th, 2015 and prints out the UNIX timestamp in seconds (should be `1448175196`).

```c
  uint32_t ts = unix_time_in_seconds( 16, 53, 06, 22, 11, 2015 );
  printf( "%d\n", ts );
```

## Notes and Limitations

It is *assumed* that the datetime given by the elements is Zulu time (GMT).  Which is to say, this function does *not* consider the following:

*  Timezones
*  Leap seconds
*  Daylight savings time

Therefore, the computed timestamp in seconds is not true "UTC" time but simply UNIX time, assuming only 86400 sec/day without compensation for changes to the planet Earth's rotation.
