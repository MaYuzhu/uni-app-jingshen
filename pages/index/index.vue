<template>
	<view class="wrap">
		
		<view class="fenge"></view>
		<view class="content1">
			<text>位移实时数据</text>
            <view class="">
            	<!-- <view id="canvasLineA"></view> -->
				<canvas canvas-id="canvasLineA" id="canvasLineA" class="charts" :style="{'width':cWidth*pixelRatio+'px',
				'height':cHeight*pixelRatio+'px', 'transform': 'scale('+(1/pixelRatio)+')','margin-left':-cWidth*(pixelRatio-1)/2+'px',
				'margin-top':-cHeight*(pixelRatio-1)/2+'px'}" @touchend="touchEndLineA"></canvas>
				
				
            </view>
 
        </view>
		<view class="fenge"></view>
		<view class="content2">
		    <text>土壤含水率实时数据</text>
		    <view class="">
		    	
		    	<canvas canvas-id="canvasLineB" id="canvasLineB" class="charts" :style="{'width':cWidth*pixelRatio+'px',
		    	'height':cHeight*pixelRatio+'px', 'transform': 'scale('+(1/pixelRatio)+')','margin-left':-cWidth*(pixelRatio-1)/2+'px',
		    	'margin-top':-cHeight*(pixelRatio-1)/2+'px'}" @touchend="touchEndLineB"></canvas>
		    	
		    	
		    </view>
		</view>
		<view class="fenge"></view>
		<view class="content3">
			
			<text>设备布点图</text>
			<view>
				<image style="width: 100%;" src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3302156260,369938832&fm=26&gp=0.jpg" mode="widthFix"></image>
			</view>
		</view>
		<view class="fenge"></view>
		<view class="content4">
		    <view class="c4_title">
				<picker class="shebei" @change="bindPickerChange" :value="index" :range="devArray">
					<view class="uni-input">{{devNum}}</view>
				</picker>
				<picker class="riqi" mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
					<view class="uni-input">{{date}}</view>
				</picker>
				<view class="sousuo">
					<uniIcon class='icon' type="search" color='#fff'></uniIcon>
				</view>
				
			</view>
			<view class="table">
				<view class="th"><text class="th1">编号</text><text class="th2">真实值</text><text class="th3">时间</text></view>
				<view class='tbody'>
					<view class="li" v-for="(item,index) in tableData" :key="index" :class="{'th_bg':index%2==0}">
						<text class="tr1">{{item.name}}</text><text class="tr2">{{item.title}}</text><text class="tr3">{{item.date}}</text>
					</view>
					
					
				</view>
			</view>
		</view>
		<view class="fenge"></view>
	</view>
</template>

<script>
	import wxCharts from '../../components/wx-charts/wxcharts.js'
	//import * as echarts from '../../static/js/echarts.min.js'
	
	import uniIcon from '../../components/uni-icon/uni-icon.vue'
	var self;
	var canvaLineA = null;
	var canvaLineB = null;
	

	export default {
		data() {
			const currentDate = this.uniGetDate({
				format: true
			})
			return {
				porjectArr:[
					{
						title:'京张高铁边坡安全监测',
						apiUrl:'https://weixin.zktop.com/jingzhang', 
						buildcode:'1101F001',
						devcodeWeiyi: '1101F00100010O08',
						devcodeShidu: '1101F00100010K03'
					},
					{
						title:'京沈高铁边坡安全监测',
						apiUrl:'https://weixin.zktop.com/jingshen', 
						buildcode:'1308F0001',
						devcodeWeiyi: '1308F00010010O09',
						devcodeShidu: '1308F00010010K01'
					},
					{
						title:'冬奥会边坡安全监测',
						//apiUrl:'http://36.110.66.218:8091', 
						//buildcode:'1308F0001',
						//devcodeWeiyi: '1308F00010010O09',
						//devcodeShidu: '1308F00010010K01'
					}
				],
					
					
				cWidth:'',
				cHeight:'',
				pixelRatio:1,
				/* 位移计数据 */
				DataTest:[
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K01",
					"devname": "T1",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 20.8
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 21.2
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 21.35
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 21.15
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 21.5
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 21
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 21.2
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 20.95
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 21.05
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 20.85
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 20.5
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 20.95
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K02",
					"devname": "T2",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.638,
					"t": 0,
					"rh": 26.2
					},
					"time": "2019-04-22 11",
					"type": null
					},
					{
					"data": {
					"v": 3.641,
					"t": 0,
					"rh": 26.9
					},
					"time": "2019-04-22 13",
					"type": null
					},
					{
					"data": {
					"v": 3.641,
					"t": 0,
					"rh": 27.2
					},
					"time": "2019-04-22 15",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 27
					},
					"time": "2019-04-22 17",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 26.5
					},
					"time": "2019-04-22 19",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 26.15
					},
					"time": "2019-04-22 21",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 26.1
					},
					"time": "2019-04-22 23",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 26
					},
					"time": "2019-04-23 01",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 25.4
					},
					"time": "2019-04-23 03",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 26
					},
					"time": "2019-04-23 05",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 25.6
					},
					"time": "2019-04-23 07",
					"type": null
					},
					{
					"data": {
					"v": 3.644,
					"t": 0,
					"rh": 25.7
					},
					"time": "2019-04-23 09",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K03",
					"devname": "T3",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 33.4
					},
					"time": "2019-04-22 13",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 33.4
					},
					"time": "2019-04-22 15",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 32.9
					},
					"time": "2019-04-22 17",
					"type": null
					},
					{
					"data": {
					"v": 3.609,
					"t": 0,
					"rh": 32.9
					},
					"time": "2019-04-22 19",
					"type": null
					},
					{
					"data": {
					"v": 3.606,
					"t": 0,
					"rh": 32.65
					},
					"time": "2019-04-22 21",
					"type": null
					},
					{
					"data": {
					"v": 3.606,
					"t": 0,
					"rh": 32.4
					},
					"time": "2019-04-22 23",
					"type": null
					},
					{
					"data": {
					"v": 3.606,
					"t": 0,
					"rh": 32.6
					},
					"time": "2019-04-23 01",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 32.65
					},
					"time": "2019-04-23 03",
					"type": null
					},
					{
					"data": {
					"v": 3.606,
					"t": 0,
					"rh": 32.5
					},
					"time": "2019-04-23 05",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 32.65
					},
					"time": "2019-04-23 07",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 32.9
					},
					"time": "2019-04-23 09",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 32.8
					},
					"time": "2019-04-23 11",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K04",
					"devname": "T4",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.615,
					"t": 0,
					"rh": 24.35
					},
					"time": "2019-04-22 11",
					"type": null
					},
					{
					"data": {
					"v": 3.615,
					"t": 0,
					"rh": 24.5
					},
					"time": "2019-04-22 13",
					"type": null
					},
					{
					"data": {
					"v": 3.615,
					"t": 0,
					"rh": 24.65
					},
					"time": "2019-04-22 15",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.65
					},
					"time": "2019-04-22 17",
					"type": null
					},
					{
					"data": {
					"v": 3.615,
					"t": 0,
					"rh": 24.5
					},
					"time": "2019-04-22 19",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.2
					},
					"time": "2019-04-22 21",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.55
					},
					"time": "2019-04-22 23",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.7
					},
					"time": "2019-04-23 01",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.85
					},
					"time": "2019-04-23 03",
					"type": null
					},
					{
					"data": {
					"v": 3.615,
					"t": 0,
					"rh": 24.4
					},
					"time": "2019-04-23 05",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.45
					},
					"time": "2019-04-23 07",
					"type": null
					},
					{
					"data": {
					"v": 3.619,
					"t": 0,
					"rh": 24.5
					},
					"time": "2019-04-23 09",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K05",
					"devname": "T5",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 28.9
					},
					"time": "2019-04-22 11",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 31.4
					},
					"time": "2019-04-22 13",
					"type": null
					},
					{
					"data": {
					"v": 3.635,
					"t": 0,
					"rh": 31.6
					},
					"time": "2019-04-22 15",
					"type": null
					},
					{
					"data": {
					"v": 3.635,
					"t": 0,
					"rh": 24.8
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.635,
					"t": 0,
					"rh": 21.6
					},
					"time": "2019-04-22 17",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 21.25
					},
					"time": "2019-04-22 19",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 20.8
					},
					"time": "2019-04-22 21",
					"type": null
					},
					{
					"data": {
					"v": 3.628,
					"t": 0,
					"rh": 20.25
					},
					"time": "2019-04-22 23",
					"type": null
					},
					{
					"data": {
					"v": 3.628,
					"t": 0,
					"rh": 20.5
					},
					"time": "2019-04-23 01",
					"type": null
					},
					{
					"data": {
					"v": 3.628,
					"t": 0,
					"rh": 20.25
					},
					"time": "2019-04-23 03",
					"type": null
					},
					{
					"data": {
					"v": 3.628,
					"t": 0,
					"rh": 20.15
					},
					"time": "2019-04-23 05",
					"type": null
					},
					{
					"data": {
					"v": 3.628,
					"t": 0,
					"rh": 19.95
					},
					"time": "2019-04-23 07",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 25.8
					},
					"time": "2019-04-23 09",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 31.2
					},
					"time": "2019-04-23 11",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K06",
					"devname": "T6",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.583,
					"t": 0,
					"rh": 20.75
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.586,
					"t": 0,
					"rh": 21.4
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.586,
					"t": 0,
					"rh": 21.4
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.586,
					"t": 0,
					"rh": 20.95
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.583,
					"t": 0,
					"rh": 20.9
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.583,
					"t": 0,
					"rh": 20.4
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.58,
					"t": 0,
					"rh": 20.4
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.58,
					"t": 0,
					"rh": 20.5
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.58,
					"t": 0,
					"rh": 20.35
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.58,
					"t": 0,
					"rh": 20
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.577,
					"t": 0,
					"rh": 20.15
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.58,
					"t": 0,
					"rh": 20.85
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K07",
					"devname": "T7",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 50.1
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 51.45
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 51.7
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 50.8
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 50.5
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 49.65
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.593,
					"t": 0,
					"rh": 49.25
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.593,
					"t": 0,
					"rh": 48.6
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.59,
					"t": 0,
					"rh": 48.9
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.59,
					"t": 0,
					"rh": 47.9
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.593,
					"t": 0,
					"rh": 47.9
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 48.6
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K08",
					"devname": "T8",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 15.35
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 15.3
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 14.85
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 15.2
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 14.95
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 14.95
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 15.4
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.599,
					"t": 0,
					"rh": 15.7
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 15.3
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 15.55
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.596,
					"t": 0,
					"rh": 15.5
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"t": 0,
					"rh": 15.8
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010K09",
					"devname": "T9",
					"devalias": "温湿度计",
					"type": "K",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 20.15
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 20.25
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.635,
					"t": 0,
					"rh": 20.1
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 20.05
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 19.25
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 19.3
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 18.95
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 18.65
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.625,
					"t": 0,
					"rh": 18.95
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.622,
					"t": 0,
					"rh": 19.1
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.628,
					"t": 0,
					"rh": 19.2
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.631,
					"t": 0,
					"rh": 19.95
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010O10",
					"devname": "L2",
					"devalias": "位移计",
					"type": "O",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.503,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.506,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.509,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.506,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.499,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.496,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.496,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.493,
					"val_l": 2332.812,
					"l": 0
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.49,
					"val_l": 2334.374,
					"l": 1.562
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.49,
					"val_l": 2334.374,
					"l": 1.562
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.496,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.499,
					"val_l": 2331.25,
					"l": -1.562
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010O11",
					"devname": "L3",
					"devalias": "位移计",
					"type": "O",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.561,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.573,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.577,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.573,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.573,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.557,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.551,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.541,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.541,
					"val_l": 2296.875,
					"l": 6.25
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.535,
					"val_l": 2296.875,
					"l": 6.25
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.538,
					"val_l": 2296.875,
					"l": 6.25
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.554,
					"val_l": 2293.749,
					"l": 3.124
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					},
					{
					"buildcode": "1308F0001",
					"devcode": "1308F00010010O12",
					"devname": "L4",
					"devalias": "位移计",
					"type": "O",
					"ztype": null,
					"status": "0",
					"devlon": 0,
					"devlat": 0,
					"time": null,
					"days": 0,
					"url": null,
					"data": [
					{
					"data": {
					"v": 3.59,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-22 12",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-22 14",
					"type": null
					},
					{
					"data": {
					"v": 3.602,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-22 16",
					"type": null
					},
					{
					"data": {
					"v": 3.593,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-22 18",
					"type": null
					},
					{
					"data": {
					"v": 3.577,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-22 20",
					"type": null
					},
					{
					"data": {
					"v": 3.573,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-22 22",
					"type": null
					},
					{
					"data": {
					"v": 3.561,
					"val_l": 2253.125,
					"l": -6.25
					},
					"time": "2019-04-23 00",
					"type": null
					},
					{
					"data": {
					"v": 3.554,
					"val_l": 2253.125,
					"l": -6.25
					},
					"time": "2019-04-23 02",
					"type": null
					},
					{
					"data": {
					"v": 3.557,
					"val_l": 2253.125,
					"l": -6.25
					},
					"time": "2019-04-23 04",
					"type": null
					},
					{
					"data": {
					"v": 3.551,
					"val_l": 2253.125,
					"l": -6.25
					},
					"time": "2019-04-23 06",
					"type": null
					},
					{
					"data": {
					"v": 3.554,
					"val_l": 2251.562,
					"l": -7.813
					},
					"time": "2019-04-23 08",
					"type": null
					},
					{
					"data": {
					"v": 3.586,
					"val_l": 2250,
					"l": -9.375
					},
					"time": "2019-04-23 10",
					"type": null
					}
					]
					}
				],
				Data:{
					LineA:{
						categories:[],
						series:[],
					},
					LineB:{
						categories:[],
						series:[],
					},
				},
				startTime: '',
				endTime: '',  
				/* 设备编号等 */
				devNum:'请选择设备',
				devArray: [],
				index: 0,
				date: currentDate,
				tableData:[
					/* {name:123,title:25.45,date:"2019-04-11 08"},
					{name:123,title:25.45,date:"2019-04-11 08"},
					{name:123,title:25.45,date:"2019-04-11 08"},
					{name:123,title:25.45,date:"2019-04-11 08"},
					{name:123,title:25.45,date:"2019-04-11 08"} */
				]
			}
		},
		onLoad(options) {
			self = this;
			let userinfo = uni.getStorageSync('session_id')
			console.log(userinfo)
			/* uni.getStorage({
				key: 'session_id',
				success: function(res) {
				    console.log(res.data)
					uni.request({
						//url: self.porjectArr[options.porject].apiUrl + '/user/login.shtml',
						url: self.porjectArr[options.porject].apiUrl + '/tsd/getBuildDevsData.shtml',
						header: {
						  'content-type': 'application/json;charset=UTF-8',
						  
						},
						dataType: "json",
						jsonp: "callback",
						data: {
							 username: 'admin',
							password: '123456' 
							'session_id': res.data,
							'timetype':'hour',
							'starttime':self.startTime,
							'endtime':self.endTime,
							'buildcode':self.porjectArr[options.porject].buildcode
						},
						
						success: res => {
							console.log(res)
							
						},
						fail: () => {
							uni.showToast({
								icon: 'none',
								title: '网络异常,请稍后重试'
							});
						},
						complete: () => {}
					});
				}
			}) */
			
 
			wx.setNavigationBarTitle({
			  title: self.porjectArr[options.porject].title
			})
			
			//#ifdef H5 || MP-ALIPAY || MP-BAIDU || MP-TOUTIAO
			uni.getSystemInfo({
			    success: function (res) {
			        if(res.pixelRatio>1){
			            self.pixelRatio =2;
			            //正常这里_self.pixelRatio给2就行，如果要求高可用下行
			            //_self.pixelRatio =res.pixelRatio;
			        }
			    }
			});
			//#endif
			this.cWidth=uni.upx2px(750);
			this.cHeight=uni.upx2px(800);
			
			//折线图数据请求
			this.startTime = this.getDate(this.getNowFormatDate(0), 0, 0, -1, 0, 0, 0)
			this.endTime = this.getNowFormatDate(0)
			//console.log(this.startTime,this.endTime)
			

			
			uni.request({
				//url: self.porjectArr[options.porject].apiUrl + '/tsd/getBuildDevsData.shtml',
				url: 'https://weixin.zktop.com/jingshen/tsd/getBuildDevsData.shtml',
				header: {
				  'content-type': 'application/json',
				  
				},
				dataType: "json",
				jsonp: "callback",
				data: {
					'timetype': 'hour',
					'starttime': '2019-04-28 13:07:22',
					'endtime': '2019-04-29 13:07:22',
					'buildcode': '1308F0001'
					/* 'timetype':'hour',
					'starttime':self.startTime,
					'endtime':self.endTime,
					'buildcode':self.porjectArr[options.porject].buildcode */
				},
				
				success: res => {
					console.log(res)
					let weiyi = self.DataTest.filter((item)=>{
						return item.type == 'O'
					})
					let shidu = self.DataTest.filter((item)=>{
						return item.type == 'K'
					})
					
					for(let i=0;i<self.DataTest.length;i++){
						self.devArray.push(self.DataTest[i].devname)
					}
					
					let timeX = []
					for (let i=0;i<weiyi[0].data.length;i++){
						timeX.push(weiyi[0].data[i].time.slice(5))
					}
					self.Data.LineA.categories = timeX
					self.Data.LineB.categories = timeX
					
					let result = []
					
					for(let i=0;i<weiyi.length;i++){
						let dataRes = []
						result.push({name:weiyi[i].devname,data:dataRes})
						for(let j=0;j<weiyi[0].data.length;j++){
							dataRes.push(weiyi[i].data[j].data.l)
						}
					}
					
					self.Data.LineA.series = result
					
					let result2 = []
					
					for(let i=0;i<shidu.length;i++){
						let dataRes2 = []
						result2.push({name:shidu[i].devname,data:dataRes2})
						for(let j=0;j<shidu[0].data.length;j++){
							dataRes2.push(shidu[i].data[j].data.rh)
						}
					}
					
					self.Data.LineB.series = result2
					
					for(let j=0;j<shidu[0].data.length;j++){
						self.tableData.push({name:j+1,title:shidu[0].data[j].data.rh,date:shidu[0].data[j].time})
					}
				},
				fail: () => {
					uni.showToast({
						icon: 'none',
						title: '网络异常,请稍后重试'
					});
				},
				complete: () => {}
			});
			
		},
		
		onReady() {
		    this.showLineA("canvasLineA",this.Data.LineA);
			this.showLineB("canvasLineB",this.Data.LineB);
			
		},
		
		methods: {
			
			showLineA(canvasId,chartData){
				/* let option = {
					canvasId: canvasId,
					type: 'line',
					fontSize:11,
					legend:true,
					dataLabel:false,//点上显示数值
					background:'#FFFFFF',
					pixelRatio:self.pixelRatio,
					categories: chartData.categories,
					series: chartData.series,
					animation: true,
					enableScroll: false,//开启图表拖拽功能
					xAxis: {
						disableGrid:true,
						itemCount:4,//可不填写，配合enableScroll图表拖拽功能使用，x轴单屏显示数据的数量，默认为5个
						//scrollBackgroundColor:'#F7F7FF',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条背景颜色,默认为 #EFEBEF
						//scrollColor:'#DEE7F7',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条颜色,默认为 #A6A6A6
					},
					yAxis: {
						//disabled:true
						//gridColor:'#7cb5ec',
					},
					width: self.cWidth*self.pixelRatio,
					height: self.cHeight*self.pixelRatio,
					
					dataPointShape: true,
					extra: {
						lineStyle: 'straight'
					},
				} */
				canvaLineA=new wxCharts({
					canvasId: canvasId,
					type: 'line',
					fontSize:11,
					legend:true,
					dataLabel:false,//点上显示数值
					background:'#FFFFFF',
					pixelRatio:self.pixelRatio,
					categories: chartData.categories,
					series: chartData.series,
					animation: true,
					enableScroll: false,//开启图表拖拽功能
					xAxis: {
						disableGrid:true,
						itemCount:4,//可不填写，配合enableScroll图表拖拽功能使用，x轴单屏显示数据的数量，默认为5个
						//scrollBackgroundColor:'#F7F7FF',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条背景颜色,默认为 #EFEBEF
						//scrollColor:'#DEE7F7',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条颜色,默认为 #A6A6A6
					},
					yAxis: {
						//disabled:true
						//gridColor:'#7cb5ec',
					},
					width: self.cWidth*self.pixelRatio,
					height: self.cHeight*self.pixelRatio,
					
					dataPointShape: true,
					extra: {
						lineStyle: 'straight'
					},
				});
				
				canvaLineB=new wxCharts({
					canvasId: canvasId,
					type: 'line',
					fontSize:11,
					legend:true,
					dataLabel:false,//点上显示数值
					background:'#FFFFFF',
					pixelRatio:self.pixelRatio,
					categories: chartData.categories,
					series: chartData.series,
					animation: true,
					enableScroll: false,//开启图表拖拽功能
					xAxis: {
						disableGrid:true,
						itemCount:4,//可不填写，配合enableScroll图表拖拽功能使用，x轴单屏显示数据的数量，默认为5个
						//scrollBackgroundColor:'#F7F7FF',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条背景颜色,默认为 #EFEBEF
						//scrollColor:'#DEE7F7',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条颜色,默认为 #A6A6A6
					},
					yAxis: {
						//disabled:true
						//gridColor:'#7cb5ec',
					},
					width: self.cWidth*self.pixelRatio,
					height: self.cHeight*self.pixelRatio,
					
					dataPointShape: true,
					extra: {
						lineStyle: 'straight'
					},
				});
				
			},
			showLineB(canvasId,chartData){
				
				canvaLineB=new wxCharts({
					canvasId: canvasId,
					type: 'line',
					fontSize:11,
					legend:true,
					dataLabel:false,//点上显示数值
					background:'#FFFFFF',
					pixelRatio:self.pixelRatio,
					categories: chartData.categories,
					series: chartData.series,
					animation: true,
					enableScroll: false,//开启图表拖拽功能
					xAxis: {
						disableGrid:true,
						itemCount:4,//可不填写，配合enableScroll图表拖拽功能使用，x轴单屏显示数据的数量，默认为5个
						//scrollBackgroundColor:'#F7F7FF',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条背景颜色,默认为 #EFEBEF
						//scrollColor:'#DEE7F7',//可不填写，配合enableScroll图表拖拽功能使用，X轴滚动条颜色,默认为 #A6A6A6
					},
					yAxis: {
						//disabled:true
						//gridColor:'#7cb5ec',
					},
					width: self.cWidth*self.pixelRatio,
					height: self.cHeight*self.pixelRatio,
					
					dataPointShape: true,
					extra: {
						lineStyle: 'straight'
					},
				});
				
			},
			touchLineA(e){
				canvaLineA.scrollStart(e);
			},
			
			moveLineA(e) {
				canvaLineA.scroll(e);
			},
			touchEndLineA(e) {
				canvaLineA.scrollEnd(e);
				//下面是toolTip事件，如果滚动后不需要显示，可不填写
				canvaLineA.showToolTip(e, {
					format: function (item, category) {
						return item.name + ':' + item.data 
					}
				});
			},
			touchEndLineB(e) {
				
				canvaLineB.showToolTip(e, {
					format: function (item, category) {
						return item.name + ':' + item.data 
					}
				});
			},
			
				
			//获取时间格式
			getDate(datetime, year, month, date, hour, minute, second) {
				datetime = datetime.replace(/-/g, '/');
				var now = new Date(datetime);
				var year = now.getFullYear() + year;
				var month = now.getMonth() + month;
				var date = now.getDate() + date;
			
				var hour = now.getHours() + hour;
				var minute = now.getMinutes() + minute;
				var second = now.getSeconds() + second;
			
				var date = new Date(year, month, date, hour, minute, second);
				return this.getNowFormatDate(date);
			},
			//获取当前时间格式
			getNowFormatDate(datetime) {
				var date;
				if (datetime == 0) {
					date = new Date();
				} else {
					date = new Date(datetime);
				}
			
				var seperator1 = "-";
				var seperator2 = ":";
				var month = date.getMonth() + 1;
				var strDate = date.getDate();
				if (month >= 1 && month <= 9) {
					month = "0" + month;
				}
				if (strDate >= 0 && strDate <= 9) {
					strDate = "0" + strDate;
				}
				var Hours = date.getHours()
				var Minutes = date.getMinutes()
				var Seconds = date.getSeconds()
			
				if (Hours >= 0 && Hours <= 9) {
					Hours = "0" + Hours;
				}
				if (Minutes >= 0 && Minutes <= 9) {
					Minutes = "0" + Minutes;
				}
				if (Seconds >= 0 && Seconds <= 9) {
					Seconds = "0" + Seconds;
				}
			
				var currentdate = date.getFullYear() + seperator1 + month + seperator1 + strDate
					+ " " + Hours + seperator2 + Minutes
					+ seperator2 + Seconds;
				return currentdate;
			},
			
			bindPickerChange(e) {
				console.log('picker发送选择改变，携带值为：' + e.target.value)
				this.index = e.target.value
				this.devNum = this.devArray[e.target.value]
			},
			
			uniGetDate(type) {
				const date = new Date();
			
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();
			
				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year ;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
			
				return `${year}-${month}-${day}`;
			},
			bindDateChange: function(e) {
				this.date = e.target.value
			},
		
		
		},
		components: {
			uniIcon
			
		},
		computed: {
			startDate() {
				return this.uniGetDate('start');
			},
			endDate() {
				return this.uniGetDate('end');
				//return this.uniGetDate({format: true})
				
			}
		},
	}
	

</script>

<style>
	.content1 text,.content2 text,.content3 text{
		font-size: 28upx;
		padding: 5px 12px;
		display: inline-block;
	}
	
	#canvasLineA,#canvasLineB{
		width: 100%;
		height: 500upx;
		
	}
	
	.c4_title{
		padding: 30upx 20upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.c4_title>picker{
		border: 1px solid #aaa;
		border-radius: 16upx;
		text-align: center;
		margin: 0 8px;
		font-size: 26upx;
		height: 50upx;
		line-height: 50upx;
	}
	.shebei,.riqi{
		width: 40%;
	}
	.c4_title>.sousuo{
		width: 20%;
		margin: 0 8px;
		background: #43aea8;
		border: 1px solid #43aea8;
		border-radius: 16upx;
		text-align: center;
		height: 50upx;
		display: table-cell;
		
	}
	.sousuo .uni-icon{
		display: block;
		font-size: 40upx;
		line-height: 50upx;
	}
	
	.c4_title>.sousuo:active{
		background: #50D0CA;
		border: 1px solid #50D0CA;
	}
	.table{
		padding: 30upx 60upx 60upx;
		font-size: 32upx;
	}
	.table .th,.tbody .li{
		display: flex;
		text-align: center;
	}
	.table .th{
		font-weight: bold;
		border-bottom: 3upx solid #ddd;
		height: 60upx;
	}
	.tbody .li{
		border-top: 3upx solid #ddd;
		height: 60upx;
		line-height: 60upx;
	}
	.th_bg{
		background: #f0f0f0;
	}
	.table .th1,.table .th2,.table .th3{
		display: block;
	}
	.table .th1{
		width: 25%;
	}
	.table .th2{
		width: 25%;
	}
	.table .th3{
		width: 50%;
		
	}
	.tbody .tr1,.tbody .tr2,.tbody .tr3{
		display: block;
	}
	.tbody .tr1{
		width: 25%;
	}
	.tbody .tr2{
		width: 25%;
	}
	.tbody .tr3{
		width: 50%;
	}
	.fenge{
		width: 100%;
		height: 40upx;
		background: #eee;
	}
</style>
