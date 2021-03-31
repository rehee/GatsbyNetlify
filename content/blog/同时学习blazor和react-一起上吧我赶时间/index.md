---
title: 同时学习blazor和react 一起上吧我赶时间
date: 2021-03-31T08:18:50.051Z
description: 学习
---
## 时间有限学习还是要增加效率

在目前的公司已经2,3年了.一直用古老的knockout和jquery. 很多流行的框架都已经发生了翻天覆地的变化. 比如blazor 都已经出了很久了. 不学习更待何时.

但是每个框架和技术都学毕竟还是太花时间.我在想如果可以同时学习岂不是美哉. 对于react来说 自己官方说自己只关心视图, blazor是一个webassemby的框架. 那么为啥不用blazor处理逻辑,用react生成组件呢. 以学习为目的同时可以学习到2样东西多好.

先弄了几天吧项目弄了起来. 直接创建了一个新的blazor webassembly项目. 然后在项目里面创建一个clientapp的文件夹用来放置react. 配置好typescript和webconfig. 这样可以将生成的文件打包. 最后在 project file里面做好配置.每次build的时候运行webpack将react准备好并放入wwwroot的dist下. 这样直接就可以同时使用blazor 和rezct了