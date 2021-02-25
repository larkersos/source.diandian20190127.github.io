title: hexo搜索无反应
author: 洛克
tags:
  - '2020'
  - hexo
categories: []
date: 2020-04-02 23:41:00
---
## hexo 搜索问题
重新安装了hexo后，发布主题，发现hexo中的search框没有反应。分析问题是插件问题
解决办法，重新安装插件后发布
		
        npm install hexo-generator-searchdb -save
        hexo g
        hexo s