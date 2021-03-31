---
title: 的确可以同时使用blazor和react
date: 2021-03-31T08:34:16.172Z
description: 增加学习效率
---
果然如我所料.

对于react来说 property数据是由父至子单向传递的,然后子在由回调Callback 回父. 这样对于整个blazor来说 blazor的组件/page就是最外一层的父组件. 然后在c# 端生成数据传递给react. 创建组件. 并且此时可以将回调对象一并送入. 这时 react接受到了由c# 传来的数据(包括callback) 根据数据生成组件. 

然后由于对于react来说 c# 穿过来新的数据就是再次进行了update 而不是重新调用一次构造器重新在渲染一个组件. status仍然保留只是更新了property. 由于本身react  就是单向传递数据. 需要callback对父进行回调. 正好和blazor可以将自己作为一个reference传递给react让它callback自己. 到目前为止感觉都完美..

当然这没算路由... 我还不知道路由和状态管理会不会乱...

github 的地址在这里. 

https://github.com/rehee/LearnReact