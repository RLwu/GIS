## GIS基础知识

### GIS基本组件

* **地图数据库**：提供地图数据，例如OSM的planet.osm可以导入PostgreSQL作为地图数据库

* **瓦片服务器**：负责生成一系列的瓦片（tiles），这些瓦片通常为256像素的方块，瓦片组在一起形成地图。对于Google Map，瓦片服务器是Google提供的，用户不能接触其地图数据库；对于OSM，地图数据库是开放的，可以随意下载，需要自己搭建瓦片服务器

* **前端API**：用于浏览器的JavaScript API，或者用于移动客户端的同功API。例如OpenLayers、Leaflet。


### 坐标参考系统（Coordinate Reference Systems）

又称空间参考系统（spatial reference system，SRS），是基于二维坐标的，用于定位局部、区域或者全球地理信息资源的体系。CRS定义了一种地图映射规则、与其它CRS之间进行转化的算法。CRS是GIS系统的基础。

最常用的两种CRS为：

<table>
<thead>
<th>CRS</th>
<th>说明</th>
</thead>
<tbody>
<tr>
<td>EPSG:4326</td>
<td>
以经纬度直接作为X（经度）、Y（维度）坐标，南纬、西经采用负数表示<br/>
投影范围: -180.0000, -85.0600, 180.0000, 85.0600
</td>
</tr>
<tr>
<td>EPSG:3857</td>
<td>
主要用于Web地图等应用程序，最初由Google地图提出，故经常称为900913，基于椭圆形墨卡托（ellipsoidal Mercator ）投影<br/>
投影范围： -180.0000, -90.0000, 180.0000, 90.0000
</td>
</tr>
</tbody>
</table>


## OpenStreetMap基础知识

### OpenStreetMap的优势

* 地图数据开源，人人可以编辑，并且可以完整的下载，部署私有的地图服务器
* 内容丰富，比起ESRI Shapefiles的点、面、线，支持更多复杂的元素
* 生态圈活跃，从地图数据、数据库、地图渲染、瓦片服务器、前端API，到桌面、Web地图设计工具，具有大量优秀的开源组件

### OpenStreetMap生态圈

<img src="images/osm1.1.png"/><img src="images/osm1.2.png"/>

## 搭建地图服务器

### Windows下搭建OSM服务器的详细步骤

目前网络上的例子，大多是在Linux下搭建OSM服务器。实际项目中由于客户现场环境的限制，可能必须使用Windows Server，故本文详细记录Windows下的搭建步骤，供各位参考。

* **系统架构**

<img src="images/osm-arch.png"/>
上图中红色部分为本文主要使用的组件，我们把这些组件全部安装到一个目录%OSM_STACK%下

* **下载地图**

区域地图，可从这里下载：[http://download.geofabrik.de/](http://download.geofabrik.de/)<br/>
全球地图，可从这里下载：[http://ftp.heanet.ie/mirrors/openstreetmap.org/planet/2015/planet-150105.osm.bz2](http://ftp.heanet.ie/mirrors/openstreetmap.org/planet/2015/planet-150105.osm.bz2)

