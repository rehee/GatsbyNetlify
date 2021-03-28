---
title: "治疗懒癌的第一步 我终于把heroku和netlify/github page的部署弄好了. "
date: 2021-03-28T11:33:46.855Z
description: 心情, 部署
---
## 跨出治疗懒癌的第一步

我本身特别喜欢c# 喜欢.net. 可是为啥就不火呢? 而且服务器还贵. 后来出.net core以后以为要翻身. 但是感觉还不火. 但是这都不是重点. 重点是友人推荐我一个叫heroku这个平台. 即使免费的等级提供的资源也挺好的. 做点小项目挺好的. 然后我上去一看发现默认没有支持.net core. 稍微搜索了一下有不少解决方案但是有点麻烦就没再弄了. 然后继续抱怨没有免费好用的服务器给我用. 作为治疗懒癌的第一步我决定从这个地方开始.

### 目标

1. 将.net core项目前后端分离
2. 将服务端发布到heroku
3. 将客户端做成spa 发布在netlify或者github page上.

### 解决方案

分离项目太简单了. 现在的都有各种的spa 框架做前端. .net core也直接就可以做后端项目.
服务端部署其实也很简单,年纪大了记性不好. 我没有使用命令行 总是记不住命令也没谁了 

1. 登录heroku, 创建app 选择github repo.
2. 在app的setting选项里面往下拖 buildpacks 的选项.选择 add buildpack
3. 在url里面直接输入大佬做的 https://github.com/jincod/dotnetcore-buildpack
4. 保存发布.

遇到的问题
大佬的脚本是会扫描repo 然后选择第一个包含start.cs或者program.cs的项目做build. 问题是我前后分离有很多项目. 我的解决方案是fork了大佬的repo https://github.com/rehee/dotnetcore-buildpack 然后修改了 文件bin/compile 将48行修改为 

```
if [ -z ${PROJECT_FILE:-} ]; then
	PROJECT_FILE=$(x=$(dirname $(find ${BUILD_DIR} -maxdepth 5 -iname .HerokuStart | head -1)); while [[ "$x" =~ $BUILD_DIR ]] ; do find "$x" -maxdepth 1 -name *.fsproj -o -name *.csproj; x=`dirname "$x"`; done)
fi
```

这样需要只需要我在想要部署的项目里面加入 名为 .HerokuStart 的空文件即可

将 spa项目部署 就简单的多了. 直接在netlify的 deploy项目中输入 donet publish 命令 然后选择输出的文件夹就可以. 关于github page 有详细的教程 https://swimburger.net/blog/dotnet/how-to-deploy-aspnet-blazor-webassembly-to-github-pages 一步步跟着走就可以.

总算完成了第一步.