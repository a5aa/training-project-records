### 1. ThinkJS

#### 1.1. 让框架支持mongdb

- 安装 ***think-mongo*** 模块

  `$ npm install think-mongo`

- 在项目的 ***config*** 目录下的 ***extend.js*** 文件中添加 ***think-mongo*** 模块

  ```
      const mongo = require('think-mongo');
  
      module.exports = [
          mongo(think.app)
      ]
  ```

#### 1.2. 创建mongodb

- 在项目 ***根目录*** 下新建 ***db*** 目录，用于存放数据

  `mkdir db`

- 开启服务

  ```
      cd db
  
      mongod --dbpath=./
  ```

  - 以后也要在此目录下开启服务，否则后台连接不上服务器

#### 1.3. 连接mongodb

- 修改 ***config*** 目录下的 ***adapter.js*** 文件

  ![avatar](https://github.com/xpcloud/training-project-records/blob/master/image/thinkjs_connet_mongo.png)

------

### 2. Flask

#### 2.1. 配置环境


        app = Flask(__name__)
        app.config['MONGO_URI'] = "mongodb://127.0.0.1:27017/db_name"
        # 实例化数据库配置，可以直接一行解决


#### 2.2. 实例化数据库

   
        mongo = PyMongo(app)