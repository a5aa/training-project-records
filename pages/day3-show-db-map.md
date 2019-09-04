
### 1. index.js代码

```
   //通用封装好的js:

var map = new BMap.Map("container"); //建树Map实例
var point = new BMap.Point(103.976032, 33.845509); // 建树点坐标
map.centerAndZoom(point, 6); // 初始化地图,设置中心点坐标和地图级别。
//地图事件设置函数：
map.enableDragging(); //启用地图拖拽事件，默认启用(可不写)
map.enableScrollWheelZoom(); //启用地图滚轮放大缩小
map.enableDoubleClickZoom(); //启用鼠标双击放大，默认启用(可不写)
map.enableKeyboard(); //启用键盘上下左右键移动地图

//向地图中添加缩放控件
var ctrl_nav = new BMap.NavigationControl({ anchor: BMAP_ANCHOR_TOP_LEFT, type: BMAP_NAVIGATION_CONTROL_LARGE });
map.addControl(ctrl_nav);
//向地图中添加缩略图控件
var ctrl_ove = new BMap.OverviewMapControl({ anchor: BMAP_ANCHOR_BOTTOM_RIGHT, isOpen: 1 });
map.addControl(ctrl_ove);
//向地图中添加比例尺控件
var ctrl_sca = new BMap.ScaleControl({ anchor: BMAP_ANCHOR_BOTTOM_LEFT });
map.addControl(ctrl_sca);
//创建marker
function addMarker() {
    for (var i = 0; i < markerArr.length; i++) {
        var json = markerArr[i];
        var p0 = json.point.split("|")[0];
        var p1 = json.point.split("|")[1];
        var point = new BMap.Point(p0, p1);
        
        var iconImg = createIcon(json.icon);
        var marker = new BMap.Marker(point, { icon: iconImg });
        map.addOverlay(marker);
    }
}
//创建一个Icon
function createIcon(json) {
    // 创建图标对象   
        //var myIcon = new BMap.Icon("../marker_red_sprite.png", new BMap.Size(23, 25), {
        //    // 指定定位位置。   
        //    // 当标注显示在地图上时，其所指向的地理位置距离图标左上    
        //    // 角各偏移10像素和25像素。您可以看到在本例中该位置即是   
        //    // 图标中央下端的尖角位置。    
        //    offset: new BMap.Size(10, 25),    
        //    // 设置图片偏移。   
        //    // 当您需要从一幅较大的图片中截取某部分作为标注图标时，您   
        //    // 需要指定大图的偏移位置，此做法与css sprites技术类似。    
        //    //imageOffset: new BMap.Size(0, 0 - index * 25)   // 设置图片偏移    
        //});
    var icon = new BMap.Icon(图片名称, new BMap.Size(json.w, json.h), { imageOffset: new BMap.Size(-json.l, -json.t), infoWindowOffset: new BMap.Size(json.lb + 5, 1), offset: new BMap.Size(json.x, json.h) })
    return icon;
}
```

### 2. 获取数据库数据

```
<html>
 <head>
  <title>百度地图加载</title>
 </head>
 <script src="Map.js"></script>
 <script type="text/javascript"> 
    
    //声明全局数组
    var markerArr = [];
    $(function () {
        //点击查询加载标注
        $("#btnSearch").click(function () {
            LoadMap();
        });

    });

    //加载游客地理位置
    function LoadMap() {
       //清空数组和所有标注点
        markerArr = [];
        map.clearOverlays();
        var par={
            startDate:$("#startDate").val(),
            endDate:$("#endDate").val()
        }
        $.ajax({
            type: "get",
            url: "/VisitorClient/GetAllInfo",
            data: par,
            dataType:"json",
            cache: false,
            success: function (r) {
                if (r.res) { 
                    dataBind(r);
                    $("#spannum").text("该时段App园区游客人数为：" + r.count);
                }
                else {
                    $("#spannum").text("该时段园区没有人使用App");
                }
                
            },
            error: function (d)
            {
                
                alert(d.responseText);
            }
        });    
    }
    function dataBind(r) {
        $.map(r.data, function (d) {
            
            var arr = { point: "" + d.Longitude + "|" + d.Latitude };
            markerArr.push(arr);
        });
        addMarker();
    }

</script>
 <body>
  <input type="button" value="搜索" id="btnSearch"/>
 </body>
</html>
```