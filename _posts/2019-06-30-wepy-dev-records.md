---
layout:     post   				    # 使用的布局（不需要改）
title:      16340049-Blasticag-Final-Project-Technical				# 标题 
subtitle:    #副标题
date:       2019-06-30				# 时间
author:     BY Blasticag				# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 系统分析与设计
---

在系分的大项目中, 我们使用了wepy框架来开发我们的小程序。

> WePY 框架在开发过程中参考了 Vue 等现有框架的一些语法风格和功能特性，对原生小程序的开发模式进行了再次封装，更贴近于 MVVM 架构模式, 并支持ES6/7的一些新特性。

wepy的这个封装使得页面结构更加清晰。

以下是使用 WePY 前后的代码对比与组件化示例:

```javascript
//原生代码 index.js
import wepy from 'wepy';

export default class Index extends wepy.page {
    getData() {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve({data: 123});
        }, 3000);
      });
    };

    async onLoad () {
      let data = await this.getData();
      console.log(data.data);
    };
}
```

```javascript
//index.wpy 中的 <script> 部分
import wepy from 'wepy';

// 通过继承自wepy.page的类创建页面逻辑
export default class Index extends wepy.page {
    //可用于页面模板绑定的数据
    data = {
      motto: 'Hello World',
      userInfo: {}
    };

    //事件处理函数(集中保存在methods对象中)
    methods = {
      bindViewTap () {
        console.log('button clicked');
      }
    };

    //页面的生命周期函数
    onLoad () {
      console.log('onLoad');
    };
}
```

这样把数据和方法分门别类放在各自的对象中, 处理起来就更方便了。

然而在实际编程中, 发现一个问题, methods中的函数之间是不能相互调用的, 要复用一个函数就必须在methos对象之外定义。这个问题始终找不到比较优美的解决方案, 希望wepy后面能解决这个问题。