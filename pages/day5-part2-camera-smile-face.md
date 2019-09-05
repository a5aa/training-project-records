
### 1. 使用微信jssdk
根据微信的开发文档，想要使用微信的jssdk，需要5个步骤
#### 1.1. 绑定域名:先登录微信公众平台进入“公众号设置”的“功能设置”里填写“JS接口安全域名”
#### 1.2. 引入JS文件
在需要调用JS接口的页面引入如下JS文件，（支持https）：http://res.wx.qq.com/open/js/jweixin-1.2.0.js  支持使用 AMD/CMD 标准模块加载方法加载
#### 1.3. 通过config接口注入权限验证配置
```
wx.config({
    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
    appId: '', // 必填，公众号的唯一标识
    timestamp: , // 必填，生成签名的时间戳
    nonceStr: '', // 必填，生成签名的随机串
    signature: '',// 必填，签名
    jsApiList: [] // 必填，需要使用的JS接口列表
});
```
#### 1.4. 通过ready接口处理成功验证
```
wx.ready(function(){
    // dosomething
});
```
 * 拍照或从手机相册中选图接口
```
wx.chooseImage({
    count: 1, // 默认9
    sizeType: ['original', 'compressed'], // 可以指定是原图还是压缩图，默认二者都有
    sourceType: ['album', 'camera'], // 可以指定来源是相册还是相机，默认二者都有
    success: function (res) {
        var localIds = res.localIds; // 返回选定照片的本地ID列表，localId可以作为img标签的src属性显示图片
    }
});
```
#### 1.5. 通过error接口处理失败验证
```
wx.error(function(res){
    // config信息验证失败会执行error函数，如签名过期导致验证失败，具体错误信息可以打开config的debug模式查看，也可以在返回的res参数中查看，对于SPA可以在这里更新签名。
});
```
### 2. 微笑检测的实现
#### 2.1. 微笑检测大概流程
* 用深度学习技术做分类
* 用OpenCV的级联分类器做人脸识别
#### 2.2. 数据介绍
* 数据地址：https://github.com/hromi/SMILEsmileD
* 数据包含13165张灰度图片，每张图片的尺寸是64*64。这个数据集并不算平衡，13165张图片中，有9475张图片不是笑脸图片，有3690张图片是笑脸图片。数据差异很大。
#### 2.3. 数据预处理
*  导入相应的包
*  解决样本不平衡问题
#### 2.4. 使用LeNet实现笑脸检测分类
* 模型实现
* 输出结果
#### 2.5. 人脸检测实现
```
from keras.preprocessing.image import img_to_array
from keras.models import load_model
import numpy as np
import imutils
import cv2
import os

haarcascade_face_dir = os.path.abspath(r"./model/haarcascade_frontalface_default.xml")
model_dir = os.path.abspath(r"./model/lenet.hdf5")
video_dir = os.path.abspath(r"./src.mp4")

detector = cv2.CascadeClassifier(haarcascade_face_dir)
model = load_model(model_dir)
camera = cv2.VideoCapture(video_dir)


while True:
    (grabbed, frame) = camera.read()

    
# grabbed和frame是read的两个返回值，grabbed是布尔类型的返回值，如果读取帧是正确的返回True，当文件读到结尾的时候返回False
# frame是每一帧的图像，是一个三维矩阵   

    frame = imutils.resize(frame, width = 300) #把图像宽度重新指定为300像素
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY) #因为模型训练是对灰度图像处理，所以这里要转换成灰度图像
    frameClone = frame.copy()    #重新克隆frame，用于接下来绘制边界框

     # scaleFactor用来控制图像金字塔， minNeighbors表示的最小特征存在数量，比如等于5表示的是有5个特征的时候才算这个人脸匹配成功
    rects = detector.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30),
                                     flags=cv2.CASCADE_SCALE_IMAGE)

 
 # .detectMultiScale方法返回一个四元组列表，来表示视频流的脸部矩形框
 # 刚开始的两个变量表示的是候选框x和y的位置，接下来两个变量的值表示的是候选框的宽度和高度  
    for (fX, fY, fW, fH) in rects:
        roi = gray[fY:fY + fH, fX:fX + fW]  # 提取灰度图像中的候选区域
        roi = cv2.resize(roi, (28, 28))   # 将候选区域变成28*28像素，接下来的操作都是便于roi用于CNN学习
        roi = roi.astype("float") / 255.0
        roi = img_to_array(roi)
        roi = np.expand_dims(roi, axis = 0)   # 扩展数组，在最开始的位置新加一个维度，便于Keras识别
        
        (notSmiling, smiling) = model.predict(roi)[0]    # 看概率，哪个概率大，就说明是笑还是不笑
        label = "Smiling" if smiling > notSmiling else "Not Smiling"
        
        cv2.putText(frameClone, label, (fX, fY - 10), cv2.FONT_HERSHEY_SIMPLEX, 
                   0.45, (0, 0, 255), 2)
        cv2.rectangle(frameClone, (fX, fY), (fX + fW, fY + fH),
                     (0, 0, 255), 2)
        
        
    cv2.imshow("Face", frameClone)  # 展示包含label的微笑判断
    
    if cv2.waitKey(1) & 0xFF == ord("q"):  # 如果 ‘q’被按下了，停止循环
        break
        
camera.release()  # 清空相机
cv2.destroyAllWindows()  # 关闭所有window
```