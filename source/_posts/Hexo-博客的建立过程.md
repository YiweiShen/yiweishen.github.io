title: ' Hexo 博客的建立过程'
date: 2015-09-30 13:14:10
tags: blog
---

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="https://music.163.com/outchain/player?type=2&id=17600647&auto=1&height=66"></iframe>

就像网上很多文章写的那样，建个 Hexo 的博客简直太方便了。本文前提：
1. Mac OS X （如果不是，请 alt+w）
2. Github 账号
3. 不能依赖本文

### 安装 Xcode (如果有必要)

### 新建 Repository
命名用 xxx.github.io (拜托请务必替换掉 xxx)
进 repo 的 settings 点击 Automatic page generator 让 Github 自动替你创建出一个 gh-pages 的页面
喝杯茶，xxx.github.io 这个网址就可以正常访问了，虽然暂时比较丑

### 安装最新 NodeJS
https://nodejs.org/download/release/latest/

### 安装 Hexo
https://hexo.io 写的很清楚
``` bash
$ npm install hexo-cli -g
$ hexo init blog
$ cd blog
$ npm install
$ hexo server
```

### 安装 NexT 主题
http://theme-next.iissnan.com/five-minutes-setup.html

``` bash
$ cd blog
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
$ hexo s
```
浏览器里可以看到 http://localhost:4000 主题已更换

### 写作及更新

``` bash
$ cd blog
$ hexo n "firstblood"
# 这将在 blog/source/_posts 文件夹下生成 firstblood.md 文件
# 选择你所中意的 Markdown 编辑器（e.g. Mou）开始码字
$ hexo d -g
# 执行之前，确保已经修改了 blog/_config.yml 中的 deploy 段
# 首次执行可能要输入 Github 账号密码
# 请参考 http://hexo.io/docs/deployment.html
```