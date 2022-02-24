title: itchat for WeChat
date: 2017-04-12 23:06:27
tags: python
---
```pythton
pip3 install itchat
```
You could find its Github page:
https://github.com/littlecodersh/itchat
This module has a complete and graceful API for WeChat.
```python
import itchat

#login on Mac terminal with white background
itchat.auto_login(enableCmdQR=-2)
```
itchat API could be found on its core.py
https://github.com/littlecodersh/ItChat/blob/master/itchat/core.py
```python
def search_friends(self, name=None, userName=None,
                   remarkName=None, nickName=None, wechatAccount=None):
    return self.storageClass.search_friends(name, userName,
                                            remarkName, nickName, wechatAccount)

def search_chatrooms(self, name=None, userName=None):
    return self.storageClass.search_chatrooms(name, userName)
    
def send_msg(self, msg='Test Message', toUserName=None):
    ''' send plain text message
        for options
            - msg: should be unicode if there's non-ascii words in msg
            - toUserName: 'UserName' key of friend dict
        it is defined in components/messages.py
    '''
    raise NotImplementedError()

# or you could use
    
def send(self, msg, toUserName=None, mediaId=None):
    ''' wrapped function for all the sending functions
        for options
            - msg: message starts with different string indicates different type
                - list of type string: ['@fil@', '@img@', '@msg@', '@vid@']
                - they are for file, image, plain text, video
                - if none of them matches, it will be sent like plain text
            - toUserName: 'UserName' key of friend dict
            - mediaId: if set, uploading will not be repeated
        it is defined in components/messages.py
    '''
    raise NotImplementedError()
```
For example, if you know the name of one particular chatroom is 'abc', then you could:
```python
some_chatroom_username = itchat.search_chatrooms(name='abc')[0]['UserName']
# then you enter the chatroom to say hi
itchat.send('Hello everyone', some_chatroom_username)
```
I know there are blank pages for previous blogs.  I know.