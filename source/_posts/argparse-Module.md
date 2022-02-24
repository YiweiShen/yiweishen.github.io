title: argparse Module
date: 2017-04-10 10:07:06
tags: python
---
```python
import argparse
```
Docs here:
https://docs.python.org/3/howto/argparse.html

The argparse module makes it easy to write user-friendly command-line interfaces.  The program defines what arguments it requires, and argparse will figure out how to parse those out of sys.argv.
```python
parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))
```