- [Day1](#day1)
    - [一、搭建Mongodb环境并建立表存储温度数据](#一搭建mongodb环境并建立表存储温度数据)
    - [二、搭建三个节点的分布式数据库](#二搭建三个节点的分布式数据库)
- [Day2](#day2)
    - [一、参考](#一参考)
        - [1. thinkjs框架](#1-thinkjs框架)
        - [2. 物流模拟](#2-物流模拟)
    - [二、后端服务](#二后端服务)
        - [1. 框架选择](#1-框架选择)
    - [三、搭建一个后端项目](#三搭建一个后端项目)
    - [四、实现后端项目与mongodb连接](#四实现后端项目与mongodb连接)
    - [五、通过后端实现对mongodb的CURD操作](#五通过后端实现对mongodb的curd操作)
    - [六、使用小程序获取地理位置的API](#六使用小程序获取地理位置的api)
    - [七、编写地理信息存储Api](#七编写地理信息存储api)
    - [八、小程序中整合二维码扫描功能](#八小程序中整合二维码扫描功能)
    - [九、传递数据到后端](#九传递数据到后端)
        - [1. 生成一个二维码](#1-生成一个二维码)
    - [十、后端对个人信息数据进行接收，存储到数据库中](#十后端对个人信息数据进行接收存储到数据库中)
- [Day 3](#day-3)
    - [一、微信小程序调用地图api](#一微信小程序调用地图api)
    - [二、百度地图获取数据库表中信息的坐标显示在地图上](#二百度地图获取数据库表中信息的坐标显示在地图上)
    - [三、在小程序中使用echarts组件](#三在小程序中使用echarts组件)
- [Day 4](#day-4)
    - [一、设计二维码](#一设计二维码)
        - [1. 参阅](#1-参阅)
    - [二、获取位置信息](#二获取位置信息)
    - [三、扫描获取二维码中的信息](#三扫描获取二维码中的信息)
    - [四、后端接收保存数据](#四后端接收保存数据)
- [Day 5](#day-5)
    - [一、目标](#一目标)
    - [二、实现](#二实现)
        - [3. 暂未实现](#3-暂未实现)
    - [三、参考：](#三参考)


# Day1

## 一、搭建Mongodb环境并建立表存储温度数据

[实现介绍](./pages/day1-db1.md)

## 二、搭建三个节点的分布式数据库

[实现介绍](./pages/day1-db2.md)


# Day2

## 一、参考

### 1. thinkjs框架

https://thinkjs.org/doc/index.html

### 2. 物流模拟

https://www.jianshu.com/p/e232c3c9af37

## 二、后端服务

### 1. 框架选择

- python + Thinkjs + mongodb
- python + flask + mongodb

## 三、搭建一个后端项目

[实现介绍](./pages/day2-part3-back-project.md)

## 四、实现后端项目与mongodb连接

[实现介绍](./pages/day2-part4-mongodb.md)
​
## 五、通过后端实现对mongodb的CURD操作

[实现介绍](./pages/day2-part5-mongodb-curd.md)

## 六、使用小程序获取地理位置的API

[实现介绍](./pages/day2-part6-get-address-api.md)

## 七、编写地理信息存储Api

[实现介绍](./pages/day2-part6-get-address-api.md)

## 八、小程序中整合二维码扫描功能

[实现介绍](./pages/day2-part8-weixin-scan.md)

## 九、传递数据到后端

### 1. 生成一个二维码

+ https://cli.im/ - 草料二维码

扫码后 将数据post给后端
参考 **7 - 编写地理信息存储API**

## 十、后端对个人信息数据进行接收，存储到数据库中

参考 **5.1.4 - thinkjs 特定 CURD 封装**

------



# Day 3

## 一、微信小程序调用地图api

[实现介绍](./pages/day3-weixin-map.md)


## 二、百度地图获取数据库表中信息的坐标显示在地图上

[实现介绍](./pages/day3-show-db-map.md)

## 三、在小程序中使用echarts组件

[实现介绍](./pages/day3-show-echarts.md)
   
# Day 4

## 一、设计二维码

### 1. 参阅

https://cli.im/ - 草料二维码

## 二、获取位置信息

[实现介绍](./pages/day4-part2-get-addr-info.md)

## 三、扫描获取二维码中的信息

[实现介绍](./pages/day4-part3-scan-info.md)

## 四、后端接收保存数据

[实现介绍](./pages/day4-part4-back-project-get-db.md)

**代码样例：**

[index.js](https://github.com/xpcloud/map-miniprogram/blob/master/pages/index/index.js)

# Day 5

## 一、目标

1. 实现拍照功能并且将图片传到后端
2. 熟悉是否微笑的相关检测并反馈给前端
3. 封装“微笑检测”为后端api

## 二、实现

[实现介绍](./pages/day5-part2-camera-smile-face.md)

### 3. 暂未实现

## 三、参考：
* https://blog.csdn.net/weixin_36882413/article/details/80674565
* https://blog.csdn.net/Einstellung/article/details/100078860 


