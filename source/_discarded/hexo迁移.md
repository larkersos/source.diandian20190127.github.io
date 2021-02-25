title: hexo迁移
author: 洛克
tags:
  - '2020'
  - hexo
  - ''
categories:
  - 技术
date: 2020-04-01 23:11:00
---
#### hexo迁移导致的一些问题
1. 找不到hexo执行命令
		ERROR Local hexo not found in D:\XXXX
        ERROR Try running: 'npm install hexo --save'

2. 分析原因是因为迁移的时候 node_models 这个文件夹不干净，导致。
      
   解决办法：
       
    	删除 node_models
    	执行 nap install
    	重新 hero g， hero s 正常启动