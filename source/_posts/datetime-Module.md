title: datetime Module
date: 2017-04-04 23:35:16
tags: python
---
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="https://music.163.com/outchain/player?type=2&id=2007819&auto=1&height=66"></iframe>

The topic today is datetime which makes me think of life.  Maybe, music is a mataphor of life.
```python
import datetime

t = datetime.date(2017, 4, 4)
t.isoweekday() # 2
t.isoformat() # '2017-04-04'

one_day = datetime.timedelta(days=1)
```
Other things useless (maybe not) you could find on
https://docs.python.org/3/library/datetime.html
```python
import time
from datetime import date

today = date.today()
today == date.fromtimestamp(time.time()) # True
my_birthday = date(today.year, 6, 24) # Fake birthday

if my_birthday < today:
    my_birthday = my_birthday.replace(year=today.year + 1)

time_to_birthday = abs(my_birthday - today) # why we need abs that makes previous IF statement meaningless
time_to_birthday.days
```
You could always find the manual. That's enough for today.