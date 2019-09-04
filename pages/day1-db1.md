### 1. 搭建环境：Ubuntu 18.04

#### 1.1. 安装下载
      sudo apt-get install mongodb
#### 1.2. 启动服务
      mongod
#### 1.3. 登陆客户端
      mongo
#### 1.4. 建立demo数据库并在其中添加存有温度信息的表
     use demo
     db.createCollection("tmp")
     db.tmp.insert({place:‘placeA’,tmp:20,time:20190901.0700})
     db.tmp.insert({place:‘placeA’,tmp:30,time:20190901.1200})
     db.tmp.insert({place:‘placeA’,tmp:24,time:20190901.2300})

### 2. 下载地址
 https://robomongo.org/down
### 3. 具体安装流程参考
 https://www.jianshu.com/p/2a76fb6e4f8b