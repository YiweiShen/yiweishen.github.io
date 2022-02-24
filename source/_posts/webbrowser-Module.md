title: webbrowser Module
date: 2017-04-03 22:50:43
tags: python
---
```python
import webbrowser

url = 'https://baidu.com'
webbrowser.open(url, new=1, autoraise=True)
webbrowser.open(url, new=0, autoraise=True)
webbrowser.open(url, new=1, autoraise=False)
webbrowser.open(url, new=0, autoraise=False)
```
Display url using the default browser. If new is 0, the url is opened in the same browser window if possible. If new is 1, a new browser window is opened if possible. If new is 2, a new browser page (“tab”) is opened if possible. If autoraise is True, the window is raised if possible (note that under many window managers this will occur regardless of the setting of this variable).

No differences among the four as far as I tested on Mac with Safari. Maybe that's because the default settings in Safari don't allow such behavior. Anyway, the below function also isn't working in terms of opening in a new window.
```python
webbrowser.open_new(url)
```
In case you want to use Chrome
```python
chrome_path = 'open -a /Applications/Google\ Chrome.app %s'
webbrowser.get(chrome_path).open(url)
```