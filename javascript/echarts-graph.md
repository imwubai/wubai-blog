

### 效果图

可点击查看大图

<a href="/public/images/1.png" target="_blank"><img style="width: 100%;" src="/public/images/1.png"></a>



1.安装依赖包

```js
npm install --save echarts-for-react
npm install --save echarts
```

2.mock接口返回数据

```js

var data = 
{
	"code": 0,
	"message": "操作成功！",
	"data": {
		"omsRequestOrderNo": "123456",
		"shippingOrderNo": null,
		"logisticsStatus": "下单",
		"plateNumber": null,
		"remark": "货主下单",
		"createDate": "2018-04-18 17:40:59",
		"operateRecordList": null,
		"children": {
			"omsRequestOrderNo": "123456",
			"shippingOrderNo": null,
			"logisticsStatus": "分配",
			"plateNumber": null,
			"remark": "分配Test测试承运商",
			"createDate": "2018-04-18 17:41:18",
			"operateRecordList": null,
			"children": {
				"omsRequestOrderNo": "123456",
				"shippingOrderNo": null,
				"logisticsStatus": "接单",
				"plateNumber": null,
				"remark": null,
				"createDate": "2018-04-18 17:42:07",
				"operateRecordList": null,
				"children": {
					"omsRequestOrderNo": "123456",
					"shippingOrderNo": "9876",
					"logisticsStatus": "完成(承运商)",
					"plateNumber": "浙B11111",
					"remark": null,
					"createDate": "2018-04-18 17:52:04",
					"operateRecordList": [{
						"omsRequestOrderNo": "123456",
						"shippingOrderNo": "9876",
						"logisticsStatus": "调度",
						"plateNumber": "浙B11111",
						"remark": "配载",
						"createDate": "2018-04-18 17:43:09",
						"operateRecordList": null,
						"children": {
							"omsRequestOrderNo": "123456",
							"shippingOrderNo": "9876",
							"logisticsStatus": "发车",
							"plateNumber": "浙B11111",
							"remark": "调度发车，车牌号：浙B11111",
							"createDate": "2018-04-18 17:45:43",
							"operateRecordList": null,
							"children": {
								"omsRequestOrderNo": "123456",
								"shippingOrderNo": "9876",
								"logisticsStatus": "发运",
								"plateNumber": "浙B11111",
								"remark": "发运",
								"createDate": "2018-04-18 17:46:21",
								"operateRecordList": null,
								"children": {
									"omsRequestOrderNo": "123456",
									"shippingOrderNo": "9876",
									"logisticsStatus": "签收",
									"plateNumber": "浙B11111",
									"remark": "卸货",
									"createDate": "2018-04-18 17:48:28",
									"operateRecordList": null,
									"children": {
										"omsRequestOrderNo": "123456",
										"shippingOrderNo": "9876",
										"logisticsStatus": "回单(承运商)",
										"plateNumber": "浙B11111",
										"remark": "回单",
										"createDate": "2018-04-18 17:52:04",
										"operateRecordList": null,
										"children": null
									}
								}
							}
						}
					}, {
						"omsRequestOrderNo": "123456",
						"shippingOrderNo": "5644",
						"logisticsStatus": "调度",
						"plateNumber": "浙B11111",
						"remark": "配载",
						"createDate": "2018-04-18 17:44:58",
						"operateRecordList": null,
						"children": {
							"omsRequestOrderNo": "123456",
							"shippingOrderNo": "5644",
							"logisticsStatus": "发车",
							"plateNumber": "浙B11111",
							"remark": "调度发车，车牌号：浙B11111",
							"createDate": "2018-04-18 17:45:29",
							"operateRecordList": null,
							"children": {
								"omsRequestOrderNo": "123456",
								"shippingOrderNo": "5644",
								"logisticsStatus": "发运",
								"plateNumber": "浙B11111",
								"remark": "发运",
								"createDate": "2018-04-18 17:46:31",
								"operateRecordList": null,
								"children": {
									"omsRequestOrderNo": "123456",
									"shippingOrderNo": "5644",
									"logisticsStatus": "签收",
									"plateNumber": "浙B11111",
									"remark": "卸货",
									"createDate": "2018-04-18 17:48:42",
									"operateRecordList": null,
									"children": {
										"omsRequestOrderNo": "123456",
										"shippingOrderNo": "5644",
										"logisticsStatus": "回单(承运商)",
										"plateNumber": "浙B11111",
										"remark": "回单",
										"createDate": "2018-04-18 17:51:31",
										"operateRecordList": null,
										"children": null
									}
								}
							}
						}
					}],
					"children": {
						"omsRequestOrderNo": null,
						"shippingOrderNo": null,
						"logisticsStatus": "回单(货主)",
						"plateNumber": null,
						"remark": null,
						"createDate": null,
						"operateRecordList": null,
						"children": {
							"omsRequestOrderNo": null,
							"shippingOrderNo": null,
							"logisticsStatus": "完成(货主)",
							"plateNumber": null,
							"remark": null,
							"createDate": null,
							"operateRecordList": null,
							"children": null
						}
					}
				}
			}
		}
	},
}
```


3.原始组件数据结构

```js
// 时间轴数据
TimeLineOptionData: {
    // tooltip: {
        // formatter: function (params) {
        //     if ( params.data.remark ) {
        //         return '备注：'+ params.data.remark;
        //     } else {
        //         return '';
        //     }
        // },
    // },
    textStyle: {
        color: '#000',
    },
    // animationDurationUpdate: 1500,
    // animationEasingUpdate: 'quinticInOut',
    series : [
        {
            type: 'graph',
            layout: 'none',
            color: ['#07b483'],
            symbolSize: 20, // 图标大小
            roam: false,
            label: {
                normal: {
                    show: true
                }
            },
            edgeSymbol: ['circle', 'arrow'],
            edgeSymbolSize: [4, 10],
            edgeLabel: {
                normal: {
                    textStyle: {
                        fontSize: 20
                    }
                }
            },
            data: [],
            links: [],
            lineStyle: {
                normal: {
                    opacity: .9,
                    width: 2,
                    curveness: 0
                }
            }
        }
    ]
},
```

4.遍历组装数据格式

```js
let _data = data.data;



let _TimeLineData = [];

/**
    *
    * @param {当前数据} nowData
    * @param {索引值} index
    */
let deepTree = function (nowData, index) {

    let _x = [0, 20, 40, 160, 180, 200];

    let _obj = {
        name: nowData.logisticsStatus,
        legendHoverLink: false,
        x: _x[index],
        y: 120,
        remark: nowData.remark,
        createDate: nowData.createDate ? nowData.createDate.slice(5, 16) : '',
        label: {
            show: true,
            position: 'bottom',
            fontSize: 14,
            distance: 20,
            formatter: function (params) {
                return params.data.name +'\n\n' + params.data.createDate;
            },
        }
    }

    if ( !nowData.createDate ) {
        // 没有时间显示灰色圆圈
        _obj.itemStyle = {
            color: '#CCC',
        }
    }

    _TimeLineData.push(_obj)

    if(nowData.children) {
        index++;
        deepTree(nowData.children, index);
    }
}
deepTree(_data, 0);

let _TimeLineDataLinks = [];
_TimeLineData.map((d, i) => {
    if ( _TimeLineData[i + 1] ) {
        if ( i == 2 ) return;
        _TimeLineDataLinks.push({
            source: d.name,
            target: _TimeLineData[i + 1].name,
        })
    }
})


// 遍历分叉数据
var operateRecordList = _data.children.children.children.operateRecordList;
if (operateRecordList && operateRecordList.length > 0) {

    let _y = [];

    // 分叉数据最多支持7条
    if ( operateRecordList.length == 1 ) {
        _y = [120]
    } else if ( operateRecordList.length == 2 ) {
        _y = [110, 130]
    } else if ( operateRecordList.length == 3 ) {
        _y = [100, 120, 140]
    } else if ( operateRecordList.length == 4 ) {
        _y = [90, 110, 130, 150]
    } else if ( operateRecordList.length == 5 ) {
        _y = [80, 100, 120, 140, 160]
    } else if ( operateRecordList.length == 6 ) {
        _y = [70, 90, 110, 130, 150, 170]
    } else if ( operateRecordList.length == 7 ) {
        _y = [60, 80, 100, 120, 140, 160, 180]
    }

    operateRecordList.map((d, i) => {
        let _array = [];
        let _deepTree = function (nowData, index) {



            let _obj = {
                name: nowData.logisticsStatus + i,
                _name: nowData.logisticsStatus,
                x: index * 20 + 60,
                y: _y[i],
                remark: nowData.remark,
                createDate: nowData.createDate ? nowData.createDate.slice(5, 16) : '',
                label: {
                    show: true,
                    position: 'bottom',
                    fontSize: 14,
                    distance: 20,
                    formatter: function (params) {
                        if ( params.data.createDate ) {
                            return params.data._name +'\n\n' + params.data.createDate;
                        } else {
                            return params.data._name;
                        }
                    },
                }
            }

            if ( !nowData.createDate ) {
                // 没有时间显示灰色圆圈
                _obj.itemStyle = {
                    color: '#CCC',
                }
            }

            _array.push(_obj);


            if(nowData.children) {
                index++;
                _deepTree(nowData.children, index);
            }
        }
        _deepTree(d, 0);
        _TimeLineData.push(..._array);

        // 从第3个分出去的分支线
        let _links = [{
            source: _TimeLineData[2].name,
            target: _array[0].name,
        }];
            _array.map((d, i) => {
                if ( _array[i + 1] ) {
                    _links.push({
                    source: d.name,
                    target: _array[i + 1].name,
                })
            }
        })

        // 分支线最后一个回归主线到第4个
        _links.push({
            source: _array[_array.length - 1].name,
            target: _TimeLineData[3].name,
        })
        _TimeLineDataLinks.push(..._links);

    })
}



TimeLineOptionData.series[0].data = _TimeLineData;
TimeLineOptionData.series[0].links = _TimeLineDataLinks;
```


5.组件调用

```js
<ReactEcharts
    option={TimeLineOptionData}
    notMerge={true}
    lazyUpdate={true}
    theme={"light"}
/>
```
