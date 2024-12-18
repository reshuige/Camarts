### 低仿翁天信 camarts 旅行足迹地图源码介绍

完全的低仿，时间多的，可以用©Mapbox ©OpenStreetMap去自己搞一个。

Mapbox 是一个提供地图制作和地理空间数据可视化服务的平台。它提供了一系列的工具，包括地图设计、数据处理和开发接口等。
OpenStreetMap 是一个由全球志愿者创建和维护的开源地图项目。它的数据是由众多志愿者通过实地考察、卫星图像解读等方式收集而来



效果图链接：![xgt](https://github.com/reshuige/Camarts/blob/main/xgt.png)

 
#### 地图初始化部分
- **引入百度地图 API**：
借助`<script>`标签引入百度地图的 API 脚本，它是调用百度地图各类接口与对象，实现相关功能的基础。

使用者需自行注册百度的 API，注册地址为控制台 | 百度地图开放平台，且要将其替换为自己申请的内容。https://lbsyun.baidu.com/apiconsole/key

![api]((https://github.com/reshuige/Camarts/blob/main/images/uid.png?raw=true))

![api]((https://github.com/reshuige/Camarts/blob/main/images/api.png?raw=true))


- **创建地图实例并设置基本属性**：
运用`new BMapGL.Map("map")`创建地图实例，并挂载到页面中`id`为`map`的`div`元素上。其初始中心点坐标设为大致中国中心位置（经度`108`，纬度`34`），初始缩放级别为`5`，这两者均可依据实际展示效果需求灵活调整优化，从而在初始状态较好呈现包含所有足迹位置的地图范围。同时，启用鼠标滚轮缩放功能方便用户查看不同细节程度的地图内容。

#### 足迹标记添加部分
- **定义足迹位置数据**：
构建名为`markersData`的数组，数组内各元素均为对象，对象涵盖足迹位置的经纬度信息（在百度地图里先经度后纬度，与原代码格式对应）以及对应的城市名称，该数据结构和原`jVectorMap`库中配置足迹标记的数据结构类似，利于后续遍历添加标记操作。
- **遍历添加标记及交互逻辑**：
利用`forEach`方法遍历`markersData`数组，针对每个元素执行如下操作：
    - 依据经纬度信息创建对应的`BMapGL.Point`坐标点对象，再通过`new BMapGL.Marker`基于该坐标点创建标记，并添加到地图上（通过`map.addOverlay(marker)`语句实现），以此在地图上展示相应的足迹位置标记。
    - 为各标记添加点击事件监听，当点击标记时，创建`BMapGL.InfoWindow`信息窗口，窗口内容为对应的城市名称，随后借助`map.openInfoWindow(infoWindow, point)`在点击的标记位置弹出显示城市名称的信息窗口，达成类似原代码中点击标记查看对应地点信息的交互效果。
技术相关
地图可能基于百度地图、百度智图、OpenStreetMap 等技术实现（根据图中文字推测）。
整体效果呈现了旅行足迹的可视化，方便用户记录和展示旅行经历。



