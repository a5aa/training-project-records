# 在小程序中使用echarts组件

### 1. 实现方法

1. 下载 GitHub 上的 ecomfe/echarts-for-weixin 项目，下载后将ec-canvas文件夹复制到小程序项目中，假设放在根目录下utils文件夹中。

2. 在要实现echarts图的页面引入echarts.js文件，例如要在index页面中展现echarts图的话，就在index.js文件中引入。

   `import * as echarts from '../../utils/ec-canvas/echarts';`

3. 在index.json中设置使用组件组件。

```
{
	"usingComponents": {
		"ec-canvas": "../../utils/ec-canvas/ec-canvas"
	}
}
```

4. 在index.wxml中使用组件<ec-canvas>

```
<view class='radar' style="width: 500rpx; height: 500rpx;">
	<ec-canvas id="mychart-dom-radar" canvas-id='mychart-line' ec="{{ec}}"></ec-canvas>
</view>
```

5. 在index.js中实现echarts具体设置，具体设置可参考echarts配置项手册和官方实例

```
function getOption(xData, data_cur, data_his) {
  var option = {
    backgroundColor: "#f5f4f3",
    color: ["#37A2DA", "#f2960d", "#67E0E3", "#9FE6B8"],
    title: {
      text: '温度变化',
      textStyle: {
        fontWeight: '500',
        fontSize: 15,
        color: '#000'
      },
      x:'center',
      y:'0'
    },
    legend: {
      data: ['今日'],
      right: 10
    },
    grid: {
      top: '15%',
      left: '1%',
      right: '3%',
      bottom: '60rpx',
      containLabel: true
    },
    tooltip: {
      show: true,
      trigger: 'axis'
    },
    xAxis: {
      type: 'time',
      boundaryGap: false,
      data: xData||[],
      axisLabel: {
        interval: 11,
        formatter: function (value, index) {
          return value.substring(0, 2) * 1;
        },
        textStyle: {
          fontsize: '10px'
        }
      }
    },
    yAxis: {
      x: 'center',
      name: 'C',
      type: 'value',
      min: 0,
      max: 40,
    },
    series: [{
      name: '今日',
      zIndex:2,
      type: 'line',
      smooth: true,
      symbolSize: 0,
      data: data_cur||[]
    }
    }]
  };
  return option;
}
```

6. 页面page中的data初始化

```
let chartLine;
Page({
    data: {
        ecLine: {
            onInit: function (canvas, width, height){
                //初始化echarts元素，绑定到全局变量，方便更改数据
                chartLine = echarts.init(canvas, null, {
                    width: width,
                    height: height
                });
                canvas.setChart(chartLine);

                //可以先不setOption，等数据加载好后赋值，
                //不过那样没setOption前，echats元素是一片空白，体验不好。
                var xData = arrayTime(5).slice(100);
                var option = getOption(xData);
                chartLine.setOption(option);
            }
        }
    }
})
```

7. 将建立的echats对象绑定到echarts元素中

```
<view class="echart_panel">
  <ec-canvas ec="{{ ecLine }}"></ec-canvas>
</view>
```

8. 然后就可以在数据加载后，给图表赋值option了，或者是重新setOption的数据

```
 //ajax请求好数据后，调用获取option函数，传一些数据，
//然后用全局变量echarts元素chartLine 来 setOption即可。
var option = getOption(xData, data_cur, data_his);
chartLine.setOption(option);
//如果上面初始化时候，已经chartLine已经setOption了，
//那么建议不要重新setOption，官方推荐写法，重新赋数据即可。
chartLine.setOption({
    xAxis: {
        data: xData
    }, 
    series: [{
        data: data_cur
    }, {
        data: data_his
    }]
});  
```
