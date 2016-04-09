---
title: how to configure your hexo blog
date: 2016-03-24 14:23:46
tags: hexo
categories: hexo

---

*Mainly reference *
* ###### Step one  `Build your own hexo on github:`
	* [使用Hexo搭建个人博客(基于hexo3.0](http://opiece.me/2015/04/09/hexo-guide/)** `recommand link`
	* [HEXO+Github,搭建属于自己的博客](http://www.jianshu.com/p/465830080ea9)
	* [hexo系列教程](http://zipperary.com/categories/hexo/)
	* [使用Github Pages建独立博客](http://beiyuu.com/github-pages/)
	* [在 Coding 上搭建 Hexo 个人博客！](https://segmentfault.com/a/1190000002900848#articleHeader0)
---
* ###### Step two  `Build your own hexo on github:`
	* [Next Theme](http://theme-next.iissnan.com/theme-settings.html#duoshuo-ua)
* ###### Need to remember
	* System config.yml
```
 theme: next # for theme change
	deploy: # for deploy update to server
  	type: git
  	repository:		ssh://git@github.com/username/username.github.io
  	branch: master 
```
* ###### mainly command:

`Generate static files:`
``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

`Run server:`
``` bash
$ hexo server
```
More info: [Server](https://hexo.io/docs/server.html)



`Deploy to remote sites`
``` bash
$ hexo deploy
```


More info: [Deployment](https://hexo.io/docs/deployment.html)

`New Post:`
``` bash
$ hexo new "xxxx" ```
* Other function: `recommand link:`[Next](http://theme-next.iissnan.com/getting-started.html)
*[多说评论](http://theme-next.iissnan.com/getting-started.html)
*[Swiftype 搜索]
*[阅读次数统计](http://tongji.baidu.com/web)
**[为NexT主题添加文章阅读量统计功能](http://notes.xiamo.tk/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)

****
#### markdown script language reference
**** [MaHua](http://mahua.jser.me/) ***
**** [markdownEditor](http://www.csdn.net/article/2014-05-05/2819623) ***
**** [theme talk](http://notes.iissnan.com/2015/something-about-next/)***
****
