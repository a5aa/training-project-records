
### 1. 准备工作

   基本流程

1. 注册账号
2. 申请开发者密钥
3. 下载SDK 

百度地图开发者平台:http://lbsyun.baidu.com

### 2. 环境配置

1. 创建本地小程序项目

2. 引入js模块

   在根目录下创建一个路径，下载百度地图微信小程序JavaScriptAPI，解压后的文件中有 bmap-wx.js 文件(压缩版 bmap-wx.min.js )，将其拷贝到新建的路径下，安装完成。

3. 请求合法域名

   登录微信公众平台－> "设置" －> "开发设置" －> "request 合法域名" －>添加 api.map.baidu.com －> 点击"保存并提交"。

### 3. 实现方法

本案例使用百度地图的**地址解析API**

**原理：** 

1. 引用百度地图微信小程序JavaScript API 模块
2. 在页面的onLoad中声明BMapWX对象
3. 调用BMapWX.geocoding方法进行地址解析

**参阅：**

[百度地图地址解析](https://lbs.baidu.com/index.php?title=wxjsapi/guide/geocoding)
