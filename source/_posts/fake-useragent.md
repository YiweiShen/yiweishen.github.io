title: fake_useragent
date: 2017-06-13 22:18:16
tags: python
---
One nice module to find.
```python
from fake_useragent import UserAgent
ua = UserAgent()
ua.random    # this would be enough
ua.update()    # once a while
```