<template>
	<view class="bg_big">
		
			<div class="image_big"><image src="../../static/loginB/bg_shou.jpg" mode=""></image></div>
			<div class="mark_big"></div>
			<div class="top">
				<div class='top_c1'><image src="../../static/loginB/loginBeforeText.png" mode="widthFix"></image></div>
				<view  class='top_c2'>
					<view class='list' value="1" @tap="navigateTo('../login/login?dev=1')">京张高铁项目</view>
					<view class='list' value="2" @tap="navigateTo('../login/login?dev=2')">京沈高铁项目</view>
					<view class='list' value="3" @tap="navigateTo('../login/login?dev=3')">冬奥会项目</view>
				</view>
			</div>
			<div class="bottom">
				<image src="../../static/loginB/annengBai.png" mode="widthFix"></image>
			</div>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			navigateTo(url){
				if (url) {
					uni.navigateTo({
						url: url
					});
				}
			}
		}
	}
</script>

<style>
page{
    width: 100%;
    height: 100%;
}
.bg_big{
    width: 100%;
    height: 100%;
    position: relative;
}
.image_big{
	position: absolute;
	width: 100%;
	height: 100%;
}
.image_big image{
	display: block;
	width: 100%;
	height: 100%;
}
.mark_big{
    width: 100%;
    height: 100%;
    position: absolute;
    background: linear-gradient(to top, rgba(200, 200, 200, 0), rgba(250, 250, 250, 1));
}
.top{
    width: 64%;
    position: absolute;
	top:40%;
	left: 50%;
	transform: translate(-50%,-50%);
    z-index: 20;
}

.top_c1{
	width: 100%;
	height: 100%;
}
.top_c1 image{
    width: 100%;
}

.top_c2{
    font-size: 16px;
}
.top_c2 .list{
    border: 1px solid #666;
    text-align: center;
    border-radius: 22px;
    padding: 8px 0;
    margin: 12px 0;
    cursor: pointer;
}
.top_c2 .li:hover{
    border: 1px solid #43aea8;
    background: #43aea8;
    color: #fff;
}
.top_c2 .li{
    border: 1px solid #43aea8;
    background: #43aea8;
    color: #fff;
}
.bottom{
    width: 120px;
    height: 36px;
    position: absolute;
    z-index: 20;
    left: 50%;
    transform: translate(-50%,0);
    bottom: 50px;
}
.bottom image{
	width: 100%;
}
</style>
