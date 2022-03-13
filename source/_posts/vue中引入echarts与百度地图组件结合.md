---
title: vue中引入echarts与百度地图组件结合
tags:
  - Vue
  - Echarts
categories:
  - Vue
  - Echarts
toc: true
abbrlink: 58764
date: 2021-07-25 12:34:20
---

## 一、新建一个vue工程

`提醒`: 先确保本地有vue相关环境,然后使用webStorm或者VSCode新建vue项目工程

<!--more-->

创建完成后，结构大致如下：

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gshnt8a9hwj30e20g4dh5.jpg" alt="image-20210715152018587" style="zoom:50%;" />



**然后右击命令行打开**，

```shell
npm install
```

```shell
npm run serve
```

启动服务



打开命令行地址页面如下：即加载成功 （我的是自己新增的组件，大家出现vue大图标的时候，表示已经可以加载成功了）

此页面也为本文所指导内容

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gshnylhp5nj31jp0u0aur.jpg" alt="image-20210715152530621" style="zoom:50%;" />



**本文共享代码仓库，文末给出**

## 二、引入Echarts

找到新创建项目的`main.js`,新增如下

```shell
import * as echarts from 'echarts'  //引入echarts基础库
import 'echarts-gl';      //引入echarts地图库

require('echarts/extension/bmap/bmap');

//定义全局挂载
Vue.prototype.$echarts = echarts
```

引入完毕，重新执行

```shell
 npm install
```

## 三、引入百度地图

在`assets`中新增目录取名`js`,新建js文件命名为`map.js`

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gsho4sazvhj30eg06c3yn.jpg" alt="image-20210715153127704" style="zoom:50%;" />

Map.js中内容如下：

```javascript
require('echarts/extension/bmap/bmap');
export function loadBMap(ak) {
    return new Promise(function(resolve, reject) {
        if (typeof BMap !== 'undefined') {
            // eslint-disable-next-line no-undef
            resolve(BMap)
            return true
        }
        window.onBMapCallback = function() {
            // eslint-disable-next-line no-undef
            resolve(BMap)
        }
        let script = document.createElement('script')
        script.type = 'text/javascript'
      	// 百度地图地址
        script.src =
            'http://api.map.baidu.com/api?v=2.0&ak='+ ak +'&__ec_v__=20190126&callback=onBMapCallback'
        script.onerror = reject
        document.head.appendChild(script)
    })
}
```

## 四、新增vue初始化页面

新增vue文件取名`BinMap.vue`

具体代码如下：

```vue
<template>
	// 定义显示echarts容器
  <div class="main"></div>
</template>


<script>
  //引入百度地图js文件
import { loadBMap } from '../assets/js/map.js'
export default {
  name: "BinMap",
  data: function (){
    return {
    }
  },
  mounted() {
    this.$nextTick(()=>{
      // 初始化地图对象
      loadBMap("57UKDCaftQhrdfWGrGUGbRGMAgjYFnOu").then(() => {
        // 实例化对象
        let myChart = this.$echarts.init(document.querySelector(".main"));

        //定义color bar
        let COLORS = ["#070093", "#1c3fbf", "#1482e5", "#70b4eb", "#b4e0f3", "#ffffff"];

        let lngExtent = [39.5, 40.6];
        let latExtent = [115.9, 116.8];
        let cellCount = [50, 50];

        let cellSizeCoord = [
          (lngExtent[1] - lngExtent[0]) / cellCount[0],
          (latExtent[1] - latExtent[0]) / cellCount[1]
        ];
				
        //定义数据 由于数据过大，保存文件存储，感兴趣可以百度echarts官网查看
        var data = []

        function renderItem(params, api) {
          var lngIndex = api.value(0);
          var latIndex = api.value(1);
          var pointLeftTop = getCoord(params, api, lngIndex, latIndex);
          var pointRightBottom = getCoord(params, api, lngIndex + 1, latIndex + 1);

          return {
            type: 'rect',
            shape: {
              x: pointLeftTop[0],
              y: pointLeftTop[1],
              width: pointRightBottom[0] - pointLeftTop[0],
              height: pointRightBottom[1] - pointLeftTop[1]
            },
            style: api.style({
              stroke: 'rgba(0,0,0,0.1)'
            }),
            styleEmphasis: api.styleEmphasis()
          };
        }
        function getCoord(params, api, lngIndex, latIndex) {
          var coords = params.context.coords || (params.context.coords = []);
          var key = lngIndex + '-' + latIndex;

          // bmap returns point in integer, which makes cell width unstable.
          // So we have to use right bottom point.
          return coords[key] || (coords[key] = api.coord([
            +(latExtent[0] + lngIndex * cellSizeCoord[0]).toFixed(6),
            +(lngExtent[0] + latIndex * cellSizeCoord[1]).toFixed(6)
          ]));
        }
        let option = {
          tooltip: {},
          visualMap: {
            type: 'piecewise',
            inverse: true,
            top: 10,
            left: 10,
            pieces: [{
              value: 0, color: COLORS[0]
            }, {
              value: 1, color: COLORS[1]
            }, {
              value: 2, color: COLORS[2]
            }, {
              value: 3, color: COLORS[3]
            }, {
              value: 4, color: COLORS[4]
            }, {
              value: 5, color: COLORS[5]
            }],
            borderColor: '#ccc',
            borderWidth: 2,
            backgroundColor: '#eee',
            dimension: 2,
            inRange: {
              color: COLORS,
              opacity: 0.7
            }
          },
          series: [
            {
              type: 'custom',
              coordinateSystem: 'bmap',
              renderItem: renderItem,
              animation: false,
              emphasis: {
                itemStyle: {
                  color: 'yellow'
                }
              },
              encode: {
                tooltip: 2
              },
              data: data
            }
          ],
          bmap: {
            center: [116.46, 39.92],
            zoom: 11.8,
            roam: true,
            mapStyle: {
              styleJson: [{
                'featureType': 'water',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'land',
                'elementType': 'all',
                'stylers': {
                  'color': '#f3f3f3'
                }
              }, {
                'featureType': 'railway',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'highway',
                'elementType': 'all',
                'stylers': {
                  'color': '#999999'
                }
              }, {
                'featureType': 'highway',
                'elementType': 'labels',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'arterial',
                'elementType': 'geometry',
                'stylers': {
                  'color': '#fefefe'
                }
              }, {
                'featureType': 'arterial',
                'elementType': 'geometry.fill',
                'stylers': {
                  'color': '#fefefe'
                }
              }, {
                'featureType': 'poi',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'green',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'subway',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'manmade',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'local',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'arterial',
                'elementType': 'labels',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'boundary',
                'elementType': 'all',
                'stylers': {
                  'color': '#fefefe'
                }
              }, {
                'featureType': 'building',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'label',
                'elementType': 'labels.text.fill',
                'stylers': {
                  'color': 'rgba(0,0,0,0)'
                }
              }]
            }
          }
        };
        myChart.setOption(option)
      })
    })
  }

}
</script>

<style scoped>
.main {
  width: 1500px;
  height: 1500px;
  margin: 0px auto;
}
</style>
```

## 五、百度地图授权

1.注册并登录百度地图开放平台（http://lbsyun.baidu.com/）。

2.如所示，点击【控制台】按钮。

3.点击应用管理，我的应用，创建新的引用即可

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gshoeopajsj325h0u043c.jpg" alt="image-20210715153941661" style="zoom:50%;" />



源码地址：https://gitee.com/liuhuanhuan963019/vue_echarts.git

