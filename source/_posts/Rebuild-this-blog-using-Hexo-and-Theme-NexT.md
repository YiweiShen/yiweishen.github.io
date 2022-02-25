---
title: Rebuild this blog using Hexo and Theme NexT
date: 2022-02-24 18:08:10
tags:
---
Seven years ago, I wrote the first post in this blog to explain how to build this blog. Basically, I still use the Hexo framework for blogging. Here is the summary of how you can rebuild the blog today.

# Versions
- Node.js v17.6.0
- npm 8.5.1
- hexo 6.0.0
- hexo-theme-next 8.10.0

If you use the different versions, things may break.

# Create GitHub Repo for the blog folder
It will be convenient to use git to version control your post writings. You can just create an empty private repo. Let's call the folder as your_blog_folder/

# Create Github Repo for hosting blog Github Page
A public repo with the repo name as YOUR_NAME.github.io, YOUR_NAME here is your GitHub account name.

# Install Node, Hexo and NexT
Install Node.js with Homebrew
```bash
brew install node
```
Install Hexo and NexT with npm
```bash
npm install -g hexo-cli
npm install hexo-theme-next
```
# Initialize Hexo
Make sure you are in the target folder
```bash
cd your_blog_folder
hexo init
npm install
```
# Configure Hexo and NexT
your_blog_folder/_config.yml is the config file for Hexo, and you need to copy the config file of NexT at /node_modules/hexo-theme-next/_config.yml to the root folder of your_blog_folder/, rename it to _config.next.yml. So they are now in the same folder. Here are some of the key configuration changes. 

For _config.yml
```bash
# Site
timezone: 'America/Toronto'
# URL
url: http://YOUR_NAME.github.io
# Extensions
theme: next
# Deployment
deploy:
  type: git
  repo: https://github.com/YOUR_NAME/YOUR_NAME.github.io
  branch: main
```
For _config.next.yml
```bash
# Creative Commons 4.0 International License.
creative_commons:
  sidebar: true
  post: true
# Menu Settings
menu:
  home: / || fa fa-home
  archives: /archives/ || fa fa-archive
# Sidebar Settings
sidebar:
  position: right
# Social Links
social:
  GitHub: https://github.com/YOUR_NAME || fab fa-github
# Subscribe through Telegram Channel, Twitter, etc.
follow_me:
  RSS: /atom.xml || fa fa-rss
# Misc Theme Settings
codeblock:
  theme:
    light: tomorrow-night-bright
    dark: tomorrow-night-bright
  copy_button:
    enable: true
    style: mac
# Reading progress bar
reading_progress:
  enable: true
```
# Write a post
```bash
hexo n 'Your_post_name'
```
And if you are using vscode, you will find the Your_post_name.md in the your_blog_folder/source/_posts/ you can write in markdown.
# Generate the post html
```
hexo g
```
You can view the post locally and make changes if you need.
# Deploy the post to GitHub
```bash
hexo d
```
It will automatically generate GitHub Page for you which you can see by visiting YOUR_NAME.github.io

When you try to deploy the blog, if you see this message ERROR Deployer not found: git, or other error messages, double check if you have all node_modules installed.
```bash
npm install hexo-deployer-git --save
```

Ref:

Hexo
https://hexo.io

Theme NexT
https://theme-next.js.org
