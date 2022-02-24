title: Safari 如何屏蔽 Youku 广告
date: 2015-10-06 00:51:34
tags: [mac, safari]
---

简单折腾了下，稍作记录，理论上类似的办法也适用于其他视频网站。鉴于是断人财路的手法，因此请低调使用。务必支持正版，如果是网站重度用户，建议购买会员。

### 方案一
此前一直使用的是：[妈妈再也不用担心我的macbook发烫了计划2.0Beta](http://zythum.sinaapp.com/youkuhtml5playerbookmark/)
只需优雅地在《我的收藏》里放一个书签，然后打开 Youku 具体播放页面，Command + 数字就可以跳过广告把视频正文内容直接唤出。小缺点是，每次必须动手，而且手必须要快，因为如果广告已经载入，就停不下来。

### 稍微麻烦但一劳永逸的方案二
#### 改 Hosts
``` bash
$ sudo nano /etc/hosts/
```
复制粘贴以下内容并保存退出：
127.0.0.1 atm.youku.com
127.0.0.1 fvid.atm.youku.com
127.0.0.1 html.atm.youku.com
127.0.0.1 valb.atm.youku.com
127.0.0.1 valf.atm.youku.com
127.0.0.1 valo.atm.youku.com
127.0.0.1 valp.atm.youku.com
127.0.0.1 lstat.youku.com
127.0.0.1 speed.lstat.youku.com
127.0.0.1 urchin.lstat.youku.com
127.0.0.1 stat.youku.com
127.0.0.1 static.lstat.youku.com
127.0.0.1 valc.atm.youku.com
127.0.0.1 vid.atm.youku.com
127.0.0.1 walp.atm.youku.com
#### 清空 Flash 缓存 (Safari 开发选项，清空缓存)
选择 “在允许新站点在此计算机上保存信息之前询问我”，然后找到
/Users/yourName/Library/Preferences/Macromedia/Flash Player/#SharedObjects/randomCode/static.youku.com 文件夹，新建一个任意文件（e.g. txt 文本文件）重命名为 static.youku.com （注意后缀是 .com 而不是 .txt），将它放在这个目录下
#### 重启 Safari
打开 Youku 测试，应该已经跳过了广告。
如果，我是说如果（不可能）出现“45秒”所谓黑屏警告，请在视频上右键进“设置”（注意不是“全局设置”），把 static.youku.com 本地缓存设为 100 KB

嗯就是这样。

To Do:
排版有点问题