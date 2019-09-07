# 编写地理信息存储Api

>   以从高德地图api的数据为例
>   address latitude longitude name

+ thinkjs  地理信息存储api

    ```
        module.exports = class extends Base {
            async indexAction() {
            }
            
            async adAction(){
                const repo = this.mongo('repo');  // 实例化模型
                const address = this.post('address');  // post 获取请求数据
                const name = this.post('name');
                const longitude = this.post('longitude');
                const latitude = this.post('latitude');
                await repo.add({address,name,longitude,latitude}); // 键值对同名 可省略 
                return this.success('200');
            }
        };
    ```

+ 小程序调用api 

```
    Page({
        data:{
            address:'', //地址
            latitude:'',  //经度
            longitude:'',  //纬度
            name:''  // 名字
        },
        xxx: function () {
            let that = this
            wx.request({
                //https 需要ssl 测试环境不加s
                url: 'http://127.0.0.1:端口号/控制器名/函数名',
                method: 'post',
                data: {
                    // 上传参数
                    address:that.data.address,
                    latitude:that.data.latitude,
                    longitude:that.data.longitude,
                    name:that.data.name
                },
                success(res) {
                //成功回调函数
                }
            })
        }
    })
    
```