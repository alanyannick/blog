# How to configure your hexo blog
*Mainly reference *
* ######Step one  `Build your own hexo on github:`
	* [使用Hexo搭建个人博客(基于hexo3.0](http://opiece.me/2015/04/09/hexo-guide/)** `recommand link`
	* [HEXO+Github,搭建属于自己的博客](http://www.jianshu.com/p/465830080ea9)
	* [hexo系列教程](http://zipperary.com/categories/hexo/)
	* [使用Github Pages建独立博客](http://beiyuu.com/github-pages/)
	* [在 Coding 上搭建 Hexo 个人博客！](https://segmentfault.com/a/1190000002900848#articleHeader0)
---
* ######Step two  `Build your own hexo on github:`
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

`New Post Generate:
``` bash
$ hexo new "xxxx
```
****
###markdown script language reference
**** [MaHua](http://mahua.jser.me/) ***
**** [markdownEditor](http://www.csdn.net/article/2014-05-05/2819623) ***

****
