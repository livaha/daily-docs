# 微信小程序入门教程

小程序开发文档：<https://developers.weixin.qq.com/miniprogram/dev/framework/> 

### 开始

- [申请帐号](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html#%E7%94%B3%E8%AF%B7%E5%B8%90%E5%8F%B7)

- [安装开发者工具](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html#%E5%AE%89%E8%A3%85%E5%BC%80%E5%8F%91%E5%B7%A5%E5%85%B7)

  [安装稳定版本 ](<https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html> )

  ![](https://user-gold-cdn.xitu.io/2019/6/7/16b30902b8687f96?w=432&h=131&f=png&s=14304)

  

- [你的第一个小程序](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html#%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%B0%8F%E7%A8%8B%E5%BA%8F)

- [编译预览](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html#%E7%BC%96%E8%AF%91%E9%A2%84%E8%A7%88)



### 小程序代码构成

通过上面的文档，现在开始了解代码构成介绍

1. `.json` 后缀的 `JSON` 配置文件
2. `.wxml` 后缀的 `WXML` 模板文件
3. `.wxss` 后缀的 `WXSS` 样式文件
4. `.js` 后缀的 `JS` 脚本逻辑文件



#### JSON 配置

##### [ 官方文档](<https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/code.html#JSON-%E9%85%8D%E7%BD%AE> )

JSON 是一种数据格式，并不是编程语言，在小程序中，JSON扮演的静态配置的角色 .

![](https://user-gold-cdn.xitu.io/2019/6/7/16b30a3cc3927bd6?w=481&h=458&f=png&s=47655)

以下图为例，现在我们介绍根目录下的 `app.json` 和 `project.config.json`，和 `pages/movie` 目录下的movie.json 



##### 小程序配置 app.json

`app.json` 是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等 

(当然，json文件并不能添加注释，使用时应按json格式来)

![](https://user-gold-cdn.xitu.io/2019/6/7/16b30c4a46867eeb?w=809&h=611&f=png&s=82030)

[全局配置文档](<https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html> )

##### 工具配置 project.config.json

[配置文档](<https://developers.weixin.qq.com/miniprogram/dev/devtools/projectconfig.html> )

![1559893444840](assets/1559893444840.png)





##### 页面配置 movie.json

这里的 movie.json` 其实用来表示 pages/movie目录下的 `movie.json` 这类和小程序页面相关的配置。 

![](https://user-gold-cdn.xitu.io/2019/6/7/16b30eebeeafdf60?w=915&h=247&f=png&s=27692)



[完整页面配置](<https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/page.html> )





### WXML模板

相当于html的角色

 pages/comment/comment.wxml

```html
// pages/comment/comment.wxml
<view>msg:{{msg}}</view>

<image src="{{img}}"></image>

<view wx:for="{{arr}}" wx:key="{{index}}">
{{index}} {{item}}
</view>

<view wx:for="{{list}}" wx:key="{{index}}">
{{item.name}} {{item.age}}
</view>

<view wx:if="{{isLogin}}">jerry</view>
<view wx:else>请登陆</view>

<view hidden='{{!isLogin}}'>hidden</view>
```

```
注释
wx:if 和 wx:else 只会显示成立的模块 
hidden，如果不成立也只是隐藏而
建议：如果需要频繁切换的情景下，用'hidden'
```



pages/comment/comment.js

```javascript
// pages/comment/comment.js
Page({

  /**
   * 页面的初始数据
   * 相当于react的state
   */
  data: {
    msg:"hello msg",
    img:'../../images/film.png',
    arr:['a','b','c','d'],
    list:[
      {
        name:'jack',
        age:45
      },{
        name:'kiy',
        age:4
      },{
        name:'abd',
        age:25
      }
    ],
    isLogin:true
  },

})
```



### WXSS 样式

`WXSS` 具有 `CSS` 大部分的特性，小程序在 `WXSS` 也做了一些扩充和修改。

1. 新增了尺寸单位。rpx:可以根据屏幕  宽度进行自适应，适配不同宽度的屏幕。

2. 

   ![](https://user-gold-cdn.xitu.io/2019/6/7/16b3136bd6b33bf9?w=1008&h=341&f=png&s=31685)

3. 提供了全局的样式和局部样式。和前边 `app.json`, `page.json` 的概念相同，你可以写一个 `app.wxss` 作为全局样式，会作用于当前小程序的所有页面，局部页面样式 `page.wxss` 仅对当前页面生效。

4. 此外 `WXSS` 仅支持部分 `CSS` 选择器

更详细的文档可以参考 [WXSS](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxss.html) 。



#### 如rpx demo

movie.wxml

```
<view class="box1"></view>
<view class="box2"></view>
```

movie.wxss

```
/* pages/movie/movie.wxss */
.box1{
  width: 200px;
  height: 200px;
  background: #18b;
}
.box2{
  width: 200rpx;
  height: 200rpx;
  background: #f00;
}
```

区别

![](https://user-gold-cdn.xitu.io/2019/6/7/16b313f0c3a41bca?w=929&h=456&f=png&s=39625)



#### 引入通用样式

路径为相对路径

在movie.wxss中引入 

```
@import '../../style/common.wxss
```



#### 推荐第三方样式库

WeUI,   iView Weapp , Vant Weapp



### 页面交互JS

先看wxml中的内容 

```
<button bindtap="onTapHandler" size="mini">点我加1</button>
<view>{{count}}</view>

<view class='box1'
bindtap="onTapBoxHandler">
  <view class='box2'
  bindtap="onTapChildHandler"></view>
</view>

<view class='box1'
catchtap="onTapBoxHandler">
  <view class='box2'
  catchtap="onTapChildHandler"></view>
</view>


<view class='box1'
catch:tap="onTapBoxHandler" id="123">
  <view class='box2'
  catch:tap="onTapChildHandler" id="456"></view>
</view>

```

大致效果如下图

![](https://user-gold-cdn.xitu.io/2019/6/7/16b316dbc9609908?w=1045&h=552&f=png&s=67646)

js交互文件：

```
// pages/movie/movie.js
Page({

  /**
   * 页面的初始数据
   */
  data: {
    count:0
  },
  onTapBoxHandler: function (e) {
    console.log('box click')
    console.log(e)
    console.log(e.target.id)
  },
  onTapChildHandler: function () {
    console.log('child box click')
  },
  onTapHandler: function () {
    this.setData({
      count:this.data.count+1
    })
  },
})
```

解释

```
点击事件是bindtap

微信的catchtap 用于阻止事件冒泡

catchtap也可以写在catch:tap

自定义属性为'data-id',即'data-xxx'
```







