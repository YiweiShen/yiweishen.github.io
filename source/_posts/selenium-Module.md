title: selenium Module
date: 2017-04-04 00:20:56
tags: python
---
```
pip3 install selenium
```
In macOS, if you have homebrew installed
```
brew install chromedriver
```
Then you could use Chrome in selenium like a charm.
```python
from selenium import webdriver

url = 'https://baidu.com'
webdriver.Chrome().get(url)

# or you could
browser = webdriver.Firefox()
browser.get(url)
```
One example on the documentation
https://pypi.python.org/pypi/selenium

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

browser = webdriver.Firefox() # open a new Firefox browser
browser.get('http://www.yahoo.com') # load the Yahoo homepage
assert 'Yahoo!' in browser.title # test, I suppose

elem = browser.find_element_by_name('p')  # Find the search box
elem.send_keys('seleniumhq' + Keys.RETURN) # search for “seleniumhq”

browser.quit() # close the browser
```
Selenium WebDriver is often used as a basis for testing web applications. Here is a simple example uisng Python’s standard unittest library:
```python
import unittest

class GoogleTestCase(unittest.TestCase):

    def setUp(self):
        self.browser = webdriver.Firefox()
        self.addCleanup(self.browser.quit)

    def testPageTitle(self):
        self.browser.get('http://www.google.com')
        self.assertIn('Google', self.browser.title)

if __name__ == '__main__':
    unittest.main(verbosity=2)
```
One more thing: selenium.webdriver.common.keys
```python
class selenium.webdriver.common.keys.Keys

ADD = u'\ue025'
ALT = u'\ue00a'
ARROW_DOWN = u'\ue015'
ARROW_LEFT = u'\ue012'
ARROW_RIGHT = u'\ue014'
ARROW_UP = u'\ue013'
BACKSPACE = u'\ue003'
BACK_SPACE = u'\ue003'
CANCEL = u'\ue001'
CLEAR = u'\ue005'
COMMAND = u'\ue03d'
CONTROL = u'\ue009'
DECIMAL = u'\ue028'
DELETE = u'\ue017'
DIVIDE = u'\ue029'
DOWN = u'\ue015'
END = u'\ue010'
ENTER = u'\ue007'
EQUALS = u'\ue019'
ESCAPE = u'\ue00c'
F1 = u'\ue031'
F10 = u'\ue03a'
F11 = u'\ue03b'
F12 = u'\ue03c'
F2 = u'\ue032'
F3 = u'\ue033'
F4 = u'\ue034'
F5 = u'\ue035'
F6 = u'\ue036'
F7 = u'\ue037'
F8 = u'\ue038'
F9 = u'\ue039'
HELP = u'\ue002'
HOME = u'\ue011'
INSERT = u'\ue016'
LEFT = u'\ue012'
LEFT_ALT = u'\ue00a'
LEFT_CONTROL = u'\ue009'
LEFT_SHIFT = u'\ue008'
META = u'\ue03d'
MULTIPLY = u'\ue024'
NULL = u'\ue000'
NUMPAD0 = u'\ue01a'
NUMPAD1 = u'\ue01b'
NUMPAD2 = u'\ue01c'
NUMPAD3 = u'\ue01d'
NUMPAD4 = u'\ue01e'
NUMPAD5 = u'\ue01f'
NUMPAD6 = u'\ue020'
NUMPAD7 = u'\ue021'
NUMPAD8 = u'\ue022'
NUMPAD9 = u'\ue023'
PAGE_DOWN = u'\ue00f'
PAGE_UP = u'\ue00e'
PAUSE = u'\ue00b'
RETURN = u'\ue006'
RIGHT = u'\ue014'
SEMICOLON = u'\ue018'
SEPARATOR = u'\ue026'
SHIFT = u'\ue008'
SPACE = u'\ue00d'
SUBTRACT = u'\ue027'
TAB = u'\ue004'
UP = u'\ue013'
```
You should also have a look at WebDriver API
http://selenium-python.readthedocs.io/api.html