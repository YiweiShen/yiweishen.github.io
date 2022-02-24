title: import re
date: 2017-04-03 21:06:20
tags: python
---
A regular expression (or RE) specifies a set of strings that matches it; the functions in this module let you check if a particular string matches a given regular expression (or if a given regular expression matches a particular string, which comes down to the same thing).  Blah blah blah.

Again, documentation first
https://docs.python.org/3/library/re.html
as always
```python
import re
```
You cannot match a Unicode string with a byte pattern or vice-versa.

The special characters in RE
tl;ra (Too long; Read anyway) or maybe you should read the documentation directly.

'.'
(Dot.) In the default mode, this matches any character except a newline. If the DOTALL flag has been specified, this matches any character including a newline.

'^'
(Caret.) Matches the start of the string, and in MULTILINE mode also matches immediately after each newline.

'$'
Matches the end of the string or just before the newline at the end of the string, and in MULTILINE mode also matches before a newline. 

'*'
Causes the resulting RE to match 0 or more repetitions of the preceding RE, as many repetitions as are possible. ab* will match ‘a’, ‘ab’, or ‘a’ followed by any number of ‘b’s.

'+'
Causes the resulting RE to match 1 or more repetitions of the preceding RE. ab+ will match ‘a’ followed by any non-zero number of ‘b’s; it will not match just ‘a’.

'?'
Causes the resulting RE to match 0 or 1 repetitions of the preceding RE. ab? will match either ‘a’ or ‘ab’.

*?, +?, ??
The '*', '+', and '?' qualifiers are all greedy; they match as much text as possible. Sometimes this behaviour isn’t desired; if the RE <.*> is matched against <a> b <c>, it will match the entire string, and not just <a>. Adding ? after the qualifier makes it perform the match in non-greedy or minimal fashion; as few characters as possible will be matched. Using the RE <.*?> will match only <a>.

{m}
Specifies that exactly m copies of the previous RE should be matched; fewer matches cause the entire RE not to match. For example, a{6} will match exactly six 'a' characters, but not five.

{m,n}
Causes the resulting RE to match from m to n repetitions of the preceding RE, attempting to match as many repetitions as possible. 

{m,n}?
Causes the resulting RE to match from m to n repetitions of the preceding RE, attempting to match as few repetitions as possible.

'\'
Either escapes special characters (permitting you to match characters like '*', '?', and so forth), or signals a special sequence

[]
Used to indicate a set of characters.

'|'
A|B, where A and B can be arbitrary REs, creates a regular expression that will match either A or B. 

(...)
Matches whatever regular expression is inside the parentheses, and indicates the start and end of a group

(?...)
This is an extension notation (a '?' following a '(' is not meaningful otherwise). The first character after the '?' determines what the meaning and further syntax of the construct is. 

(?aiLmsux)
(One or more letters from the set 'a', 'i', 'L', 'm', 's', 'u', 'x'.) The group matches the empty string; the letters set the corresponding flags: re.A (ASCII-only matching), re.I (ignore case), re.L (locale dependent), re.M (multi-line), re.S (dot matches all), and re.X (verbose), for the entire regular expression.

(?:...)
A non-capturing version of regular parentheses. Matches whatever regular expression is inside the parentheses, but the substring matched by the group cannot be retrieved after performing a match or referenced later in the pattern.

(?imsx-imsx:...)
(Zero or more letters from the set 'i', 'm', 's', 'x', optionally followed by '-' followed by one or more letters from the same set.) The letters set or removes the corresponding flags: re.I (ignore case), re.M (multi-line), re.S (dot matches all), and re.X (verbose), for the part of the expression. (The flags are described in Module Contents.)

(?P<name>...)
Similar to regular parentheses, but the substring matched by the group is accessible via the symbolic group name name. If the pattern is (?P<quote>['"]).*?(?P=quote) (i.e. matching a string quoted with either single or double quotes)

(?P=name)
A backreference to a named group; it matches whatever text was matched by the earlier group named name.

(?#...)
A comment; the contents of the parentheses are simply ignored.

(?=...)
Matches if ... matches next, but doesn’t consume any of the string. This is called a lookahead assertion. For example, Isaac (?=Asimov) will match 'Isaac ' only if it’s followed by 'Asimov'.

(?!...)
Matches if ... doesn’t match next. This is a negative lookahead assertion. For example, Isaac (?!Asimov) will match 'Isaac ' only if it’s not followed by 'Asimov'.

(?<=...)
Matches if the current position in the string is preceded by a match for ... that ends at the current position. This is called a positive lookbehind assertion. (?<=abc)def will find a match in abcdef, since the lookbehind will back up 3 characters and check if the contained pattern matches. The contained pattern must only match strings of some fixed length, meaning that abc or a|b are allowed, but a* and a{3,4} are not. 

(?<!...)
Matches if the current position in the string is not preceded by a match for ...

(?(id/name)yes-pattern|no-pattern)
Will try to match with yes-pattern if the group with given id or name exists, and with no-pattern if it doesn’t. no-pattern is optional and can be omitted. For example, (<)?(\w+@\w+(?:\.\w+)+)(?(1)>|$) is a poor email matching pattern, which will match with '<user@host.com>' as well as 'user@host.com', but not with '<user@host.com' nor 'user@host.com>'.

\number
Matches the contents of the group of the same number. Groups are numbered starting from 1. For example, (.+) \1 matches 'the the' or '55 55', but not 'thethe' (note the space after the group).

\A
Matches only at the start of the string.

\b
Matches the empty string, but only at the beginning or end of a word.

\B
Matches the empty string, but only when it is not at the beginning or end of a word. This means that r'py\B' matches 'python', 'py3', 'py2', but not 'py', 'py.', or 'py!'. 

\d
For Unicode (str) patterns:
Matches any Unicode decimal digit (that is, any character in Unicode character category [Nd]). This includes [0-9], and also many other digit characters. If the ASCII flag is used only [0-9] is matched (but the flag affects the entire regular expression, so in such cases using an explicit [0-9] may be a better choice).
For 8-bit (bytes) patterns:
Matches any decimal digit; this is equivalent to [0-9].

\D
Matches any character which is not a Unicode decimal digit. This is the opposite of \d. If the ASCII flag is used this becomes the equivalent of [^0-9] (but the flag affects the entire regular expression, so in such cases using an explicit [^0-9] may be a better choice).

\s
Matches Unicode whitespace characters 

\S
Matches any character which is not a Unicode whitespace character.

\w
Matches Unicode word characters

\W
Matches any character which is not a Unicode word character.

\Z
Matches only at the end of the string.

OK, let's move on to Module Contents
```python
re.compile(pattern, flags=0)
```
Compile a regular expression pattern into a regular expression object, which can be used for matching using its match() and search() methods
```python
prog = re.compile(pattern)
result = prog.match(string)
```
is equivalent to
```python
result = re.match(pattern, string)
```
but using re.compile() and saving the resulting regular expression object for reuse is more efficient when the expression will be used several times in a single program.

re.A
re.ASCII

re.DEBUG

re.I
re.IGNORECASE

re.L
re.LOCALE

re.M
re.MULTILINE

re.S
re.DOTALL

re.X
re.VERBOSE
This flag allows you to write regular expressions that look nicer and are more readable by allowing you to visually separate logical sections of the pattern and add comments. Whitespace within the pattern is ignored, except when in a character class or when preceded by an unescaped backslash. When a line contains a # that is not in a character class and is not preceded by an unescaped backslash, all characters from the leftmost such # through the end of the line are ignored.

This means that the two following regular expression objects that match a decimal number are functionally equal:
```python
a = re.compile(r"""\d +  # the integral part
                   \.    # the decimal point
                   \d *  # some fractional digits""", re.X)
b = re.compile(r"\d+\.\d*")

re.search(pattern, string, flags=0)
```
Scan through string looking for the first location where the regular expression pattern produces a match, and return a corresponding match object.
```python
re.match(pattern, string, flags=0)
```
If zero or more characters at the beginning (be careful) of string match the regular expression pattern, return a corresponding match object. 
```python
re.fullmatch(pattern, string, flags=0)
```
If the whole string matches the regular expression pattern, return a corresponding match object. 
```python
re.split(pattern, string, maxsplit=0, flags=0)
# Split string by the occurrences of pattern.
re.split('\W+', 'Words, words, words.')
# ['Words', 'words', 'words', '']
re.split('(\W+)', 'Words, words, words.')
# ['Words', ', ', 'words', ', ', 'words', '.', '']
re.split('\W+', 'Words, words, words.', 1)
# ['Words', 'words, words.']
re.split('[a-f]+', '0a3B9', flags=re.IGNORECASE)
# ['0', '3', '9']
re.split('(\W+)', '...words, words...')
# ['', '...', 'words', ', ', 'words', '...', '']

re.findall(pattern, string, flags=0)
# Return all non-overlapping matches of pattern in string, as a list of strings.

re.finditer(pattern, string, flags=0)
# Return an iterator yielding match objects over all non-overlapping matches for the RE pattern in string.

re.sub(pattern, repl, string, count=0, flags=0)
```
Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl.
```python
m = re.match(r"(\w+) (\w+)", "Isaac Newton, physicist")
m.group(0)       # The entire match 'Isaac Newton'
m.group(1)       # The first parenthesized subgroup. 'Isaac'
m.group(2)       # The second parenthesized subgroup. 'Newton'
m.group(1, 2)    # Multiple arguments give us a tuple. ('Isaac', 'Newton')

email = "tony@tiremove_thisger.net"
m = re.search("remove_this", email)
email[:m.start()] + email[m.end():]
# 'tony@tiger.net'
```
Regular Expression Examples in standard docs
```python
def displaymatch(match):
    if match is None:
        return None
    return '<Match: %r, groups=%r>' % (match.group(), match.groups())
```
Suppose you are writing a poker program where a player’s hand is represented as a 5-character string with each character representing a card, “a” for ace, “k” for king, “q” for queen, “j” for jack, “t” for 10, and “2” through “9” representing the card with that value.

To see if a given string is a valid hand, one could do the following:
```python
valid = re.compile(r"^[a2-9tjqk]{5}$")
displaymatch(valid.match("akt5q"))  # Valid. "<Match: 'akt5q', groups=()>"
displaymatch(valid.match("akt5e"))  # Invalid.
displaymatch(valid.match("akt"))    # Invalid.
displaymatch(valid.match("727ak"))  # Valid. "<Match: '727ak', groups=()>"
```
That last hand, "727ak", contained a pair, or two of the same valued cards. To match this with a regular expression, one could use backreferences as such:
```python
pair = re.compile(r".*(.).*\1")
displaymatch(pair.match("717ak"))     # Pair of 7s. "<Match: '717', groups=('7',)>"
displaymatch(pair.match("718ak"))     # No pairs.
displaymatch(pair.match("354aa"))     # Pair of aces. "<Match: '354aa', groups=('a',)>"
```
To find out what card the pair consists of, one could use the group() method of the match object in the following manner:
```python
pair.match("717ak").group(1) # '7'
# Error because re.match() returns None, which doesn't have a group() method:
pair.match("718ak").group(1)
Traceback (most recent call last):
  File "<pyshell#23>", line 1, in <module>
    re.match(r".*(.).*\1", "718ak").group(1)
AttributeError: 'NoneType' object has no attribute 'group'

pair.match("354aa").group(1) # 'a'
```
search() vs. match()

of course you can look up on stackoverflow: re.match() checks for a match only at the beginning of the string, while re.search() checks for a match anywhere in the string (this is what Perl does by default).
```python
text = "He was carefully disguised but captured quickly by police."
re.findall(r"\w+ly", text) # ['carefully', 'quickly']
```
Writing a Tokenizer
```python
import collections
import re

Token = collections.namedtuple('Token', ['typ', 'value', 'line', 'column'])

def tokenize(code):
    keywords = {'IF', 'THEN', 'ENDIF', 'FOR', 'NEXT', 'GOSUB', 'RETURN'}
    token_specification = [
        ('NUMBER',  r'\d+(\.\d*)?'),  # Integer or decimal number
        ('ASSIGN',  r':='),           # Assignment operator
        ('END',     r';'),            # Statement terminator
        ('ID',      r'[A-Za-z]+'),    # Identifiers
        ('OP',      r'[+\-*/]'),      # Arithmetic operators
        ('NEWLINE', r'\n'),           # Line endings
        ('SKIP',    r'[ \t]+'),       # Skip over spaces and tabs
        ('MISMATCH',r'.'),            # Any other character
    ]
    tok_regex = '|'.join('(?P<%s>%s)' % pair for pair in token_specification)
    line_num = 1
    line_start = 0
    for mo in re.finditer(tok_regex, code):
        kind = mo.lastgroup
        value = mo.group(kind)
        if kind == 'NEWLINE':
            line_start = mo.end()
            line_num += 1
        elif kind == 'SKIP':
            pass
        elif kind == 'MISMATCH':
            raise RuntimeError(f'{value!r} unexpected on line {line_num}')
        else:
            if kind == 'ID' and value in keywords:
                kind = value
            column = mo.start() - line_start
            yield Token(kind, value, line_num, column)

statements = '''
    IF quantity THEN
        total := total + price * quantity;
        tax := price * 0.05;
    ENDIF;
'''

for token in tokenize(statements):
    print(token)
```
The tokenizer produces the following output:
```python
Token(typ='IF', value='IF', line=2, column=4)
Token(typ='ID', value='quantity', line=2, column=7)
Token(typ='THEN', value='THEN', line=2, column=16)
Token(typ='ID', value='total', line=3, column=8)
Token(typ='ASSIGN', value=':=', line=3, column=14)
Token(typ='ID', value='total', line=3, column=17)
Token(typ='OP', value='+', line=3, column=23)
Token(typ='ID', value='price', line=3, column=25)
Token(typ='OP', value='*', line=3, column=31)
Token(typ='ID', value='quantity', line=3, column=33)
Token(typ='END', value=';', line=3, column=41)
Token(typ='ID', value='tax', line=4, column=8)
Token(typ='ASSIGN', value=':=', line=4, column=12)
Token(typ='ID', value='price', line=4, column=15)
Token(typ='OP', value='*', line=4, column=21)
Token(typ='NUMBER', value='0.05', line=4, column=23)
Token(typ='END', value=';', line=4, column=27)
Token(typ='ENDIF', value='ENDIF', line=5, column=4)
Token(typ='END', value=';', line=5, column=9)
```

I know, I know it's a headache to read these, try PyMOTW-3 instead if you want
https://pymotw.com/3/re/index.html

Out there is an alternative regular expression module, to replace re, called regex.
https://pypi.python.org/pypi/regex/

And read this:
10 Tips to Get More out of Your Regexes
http://pybit.es/mastering-regex.html