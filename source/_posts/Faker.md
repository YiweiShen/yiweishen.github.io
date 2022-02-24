title: Faker
date: 2017-05-16 22:28:35
tags: [python]
---
Tutorial here:
https://semaphoreci.com/community/tutorials/generating-fake-data-for-python-unit-tests-with-faker

```python
pip3 install faker # as always

from faker import Faker
f = Faker()
f.text()
dir(f) # check it out
```
For me, I think it would be a wonderful tool for generating random words or names or addresses or anything for testing or other purposes. The random module is limited in some way.