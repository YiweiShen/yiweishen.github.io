title: time Module in Python 3 Standard Library
date: 2017-04-03 19:39:21
tags: python
---

According to 16.3. time — Time access and conversions
https://docs.python.org/3/library/time.html
```python
This module provides various time-related functions. 
```
Or you can say in this module there are
````python
Functions for manipulating clock time.
````
as in the PYMOTW-3
https://pymotw.com/3/time/index.html

I am not going to list every function available in the 'time' module, only the core functions such as time(), etc.

```python
import time

time.time()
```
You would see number of seconds since the start of the “epoch” as a floating point value, e.g. 1491220050.174642.
```python
time.ctime() # 'Mon Apr  3 19:49:02 2017'
time.ctime(15) # 'Thu Jan  1 08:00:15 1970'
time.ctime(1) # 'Thu Jan  1 08:00:01 1970'
time.ctime(time.time()+15) # 'Mon Apr  3 19:52:10 2017'

start = time.monotonic()
time.sleep(15.5) # sleep for at least 15.5 seconds, see PEP 475
end = time.monotonic()
```
Only the difference between the results of consecutive calls is valid. The same applies to time.perf_counter() and time.process_time()
```python
time.gmtime()
```
time.struct_time(tm_year=2017, tm_mon=4, tm_mday=3, tm_hour=12, tm_min=3, tm_sec=33, tm_wday=0, tm_yday=93, tm_isdst=0)
```python
time.gmtime().tm_year # 2017
time.gmtime()[0] # 2017

time.perf_counter()
```
Return the value (in fractional seconds) of a performance counter, i.e. a clock with the highest available resolution to measure a short duration. It does include time elapsed during sleep and is system-wide.
```python
time.process_time()
```
Return the value (in fractional seconds) of the sum of the system and user CPU time of the current process. It does not include time elapsed during sleep. It is process-wide by definition.

The above should be enough for now.