---
title: HEXO指令归纳
tags: HEXO,指令
grammar_cjkRuby: true
---


HEXO的指令归纳

HEXO安装、升级及初始化

``` stylus
npm install hexo -g     //安装
npm update hexo -g      //升级
hexo init        //初始化
```

简写

``` stylus
hexo n "我的博客" == hexo new "我的博客"    //新建文章
hexo p == hexo publish
hexo g == hexo generate     //生成静态文件
hexo s == hexo server       //启动服务预览
hexo d == hexo deploy       部署
```

服务器

``` stylus
hexo server     //hexo会监视文件变动并自动更新，您无须重启服务器
hexo server -s      //静态模式
hexo server -p 5000     //更改端口
hexo server -i 192.168.1.1      //自定义IP
hexo clean      //清除缓存
hexo g      //生成静态文件
hexo d      //开始部署
```

监视文件变动

``` stylus
hexo generate       //使用HEXO生成静态文件
hexo generate -watch        //监视文件变动
```

完成后部署

``` stylus
两个命令的作用是相同的
hexo generate --deploy
hexo deploy --generate
```

``` stylus
hexo deploy -g
hexo server -g
```









