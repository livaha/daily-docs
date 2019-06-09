# 微信云函数基础

[云开发文档](<https://developers.weixin.qq.com/miniprogram/dev/wxcloud/basis/getting-started.html> )

开发者可以使用云开发开发微信小程序、小游戏，无需搭建服务器，即可使用云端能力。



### 三大基础能力支持

云函数：获取appid,获取openid,生成分享图，调用腾讯云SDK...

云数据库：数据增加，数据删除，数据修改，数据查询...

云存储：管理文件，上传文件，下载文件，分享文件...



### 云开发服务设置

#### 1 开通云开发服务

![](https://user-gold-cdn.xitu.io/2019/6/7/16b321e7b77df0ab?w=478&h=167&f=png&s=18098)





#### 2 开通后可进入云开发控制平台

每个小程序账号可以创建2个环境，我们可以创建一个开发环境，一个生产环境，创建如下图

![](https://user-gold-cdn.xitu.io/2019/6/7/16b322174b93a648?w=1195&h=477&f=png&s=46351)



#### 3 版本库设置 

使用云开发功能，开发者工具基础库必须在2.2.3版本以上，

选择下图‘>>’，点击详情，设置基础库版本。

![](https://user-gold-cdn.xitu.io/2019/6/7/16b3223e0dcf6e2a?w=412&h=815&f=png&s=53833)



### 云开发能力

#### 数据库 [文档](<https://developers.weixin.qq.com/miniprogram/dev/wxcloud/basis/capabilities.html#%E6%95%B0%E6%8D%AE%E5%BA%93> )

| 关系型          | 文档型            |
| --------------- | ----------------- |
| 数据库 database | 数据库 database   |
| 表 table        | 集合 collection   |
| 行 row          | 记录 record / doc |
| 列 column       | 字段 field        |

#### 数据类型

云开发数据库提供以下几种数据类型：

- String：字符串
- Number：数字
- Object：对象
- Array：数组
- Bool：布尔值
- GeoPoint：地理位置点
- Date：时间
- Null



#### 权限管理 

对一个用户来说，不同模式在小程序端和管理端的权限表现如下：

 

| 模式                                   | 小程序端 读自己创建的数据 | 小程序端 写自己创建的数据 | 小程序端 读他人创建的数据 | 小程序端 写他人创建的数据 | 管理端 读写任意数据 |
| -------------------------------------- | ------------------------- | ------------------------- | ------------------------- | ------------------------- | ------------------- |
| 仅创建者可写，所有人可读               | √                         | √                         | √                         | ×                         | √                   |
| 仅创建者可读写                         | √                         | √                         | ×                         | ×                         | √                   |
| 仅管理端可写，所有人可读               | √                         | ×                         | √                         | ×                         | √                   |
| 仅管理端可读写：该数据只有管理端可读写 | ×                         | ×                         | ×                         | ×                         | √                   |



### 使用

### 创建一个集合

![](https://user-gold-cdn.xitu.io/2019/6/7/16b3231059ac1647?w=891&h=331&f=png&s=36374)

创建成功后，可以看到 `todos` 集合管理界面，界面中我们可以添加记录、查找记录、管理索引和管理权限。

 

#### 数据库demo

wxml

```
<button bindtap="insert">insert</button>
<button bindtap="update">update</button>
<button bindtap="search">search</button>
<button bindtap="delete">delete</button>
```

wxjs

```javascript
// pages/cloud/cloud.js
const db = wx.cloud.database() //初始化数据库
Page({
  /**
   * 页面的初始数据
   */
  data: {

  },

  insert: function () {
    db.collection('user').add({
      data:{
        name:"nick",
        description:"learn cloud database",
        due:new Date('2019-09-09'),
        tags:[
          "cloud",
          "database"
        ]
      }
    }).then(res=>{
      console.log(res)
    }).catch(res=>{
      console.error(res)
    })

  },
  update: function () {
    db.collection('user').doc('cbdb4c165cfa89bd016c1213527d8cbe').update({
      data:{
        name:'sbwxffnhc'
      }
    }).then(res=>{
      console.log(res)
    })
  }
  search: function () {
    db.collection('user').where({
      name:'sbwxffnhc'
    }).get().then(res=>{
      console.log(res)
    }).catch(res=>{
      console.log(res)
    })
    
  },
  delete: function () {
    db.collection('user').doc('cbdb4c165cfa89bd016c1213527d8cbe').remove()
    .then(res => {
      console.log(res)
      }).catch(res => {
        console.log(res)
      })

  }
})
```



查找：

通过自己手动创建的记录，查询不一定能找到，要通过创建权限去获得

![](https://user-gold-cdn.xitu.io/2019/6/8/16b36429cf696eb9?w=690&h=360&f=png&s=33704)



#### 云函数demo

要安装nodejs

求和函数sum()

获取当前用户的openid

批量删除云函数库的数据



##### 开始第一个云函数 [文档](<https://developers.weixin.qq.com/miniprogram/dev/wxcloud/guide/functions/getting-started.html> )

1 项目根目录找到 `project.config.json` 文件 

指定本地已存在的目录作为云函数的本地根目录

示例：

```javascript
{
	"cloudfunctionRoot": "cloudfunctions/"
}
```

2 在云函数根目录上右键，在右键菜单中，可以选择创建一个新的 Node.js 云函数，我们将该云函数命名为 add。 

修改云函数代码并返回给调用端

```javascript
exports.main = async (event, context) => {
  return {
    sum: event.a + event.b
  }
}
```

修改完后在云函数目录上右键，在右键菜单中，我们可以将云函数整体打包上传并部署到线上环境中。 

部署完成后，我们可以在小程序中调用该云函数： 

```javascript
wx.cloud.callFunction({
  // 云函数名称
  name: 'add',
  // 传给云函数的参数
  data: {
    a: 1,
    b: 2,
  },
})
.then(res => {
  console.log(res.result) // 3
})
.catch(console.error)
```

那么到这里，我们就成功创建了我们的第一个云函数，并在小程序中成功调用！



##### 获取小程序用户信息

云开发的云函数的独特优势在于与微信登录鉴权的无缝整合。当小程序端调用云函数时，云函数的传入参数中会被注入小程序端用户的 openid，开发者无需校验 openid 的正确性，因为微信已经完成了这部分鉴权，开发者可以直接使用该 openid。与 openid 一起同时注入云函数的还有小程序的 appid。 

去函数默认的函数模板：

```javascript
// 云函数入口文件
const cloud = require('wx-server-sdk')

cloud.init()

// 云函数入口函数
exports.main = async (event, context) => {
  const wxContext = cloud.getWXContext()

  return {
    event,
    openid: wxContext.OPENID,
    appid: wxContext.APPID,
    unionid: wxContext.UNIONID,
  }
}
```

在小程序端调用：

```javascript

  getopenid: function () {
    wx.cloud.callFunction({
      name: 'openid',
    })
      .then(res => {
        console.log(res)
      })
      .catch(console.error)
  },
```



![](https://user-gold-cdn.xitu.io/2019/6/9/16b3bf2fe1f4f916?w=739&h=381&f=png&s=126041)

![](https://user-gold-cdn.xitu.io/2019/6/9/16b3bf362753c93b?w=682&h=364&f=png&s=96850)



##### 通过云函数批量删除数据

云函数delete

```javascript
// 云函数入口文件
const cloud = require('wx-server-sdk')

cloud.init()

const db=cloud.database();
// 云函数入口函数
exports.main = async (event, context) => {
  try{
    return await db.collection('user').where({
      name: 'nick'
    }).remove();
  }
  catch(e){
    console.error(e)
  }
}
```



小程序端调用

```javascript

  delete: function () {
    wx.cloud.callFunction({
      name: 'delete'
    })
      .then(res => {
        console.log(res)
      })
      .catch(console.error)
  },
```

