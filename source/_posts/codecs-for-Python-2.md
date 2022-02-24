title: codecs for Python 2
date: 2017-04-10 00:31:01
tags: [python]
---
```python
# Handling Unicode: http://stackoverflow.com/a/6633040/305414
import sys
if sys.version < '3':
    import codecs
    def u(x):
        return codecs.unicode_escape_decode(x)[0]
else:
    def u(x):
        return x
```
Still search for the documentation for the function unicode_escape_decode() in codecs.