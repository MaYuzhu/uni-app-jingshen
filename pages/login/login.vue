<template>
	<view  class="bg_big">
		<div class="image_big"><image :src=bgImg mode=""></image></div>
		<div class="mark_big"></div>
		<div class="login_box">
				
				<image :src=textImgUrl alt="" mode="widthFix"></image>
				
				<div class="f1">
					<label for="user" class="label1">用户</label>
					<input id="user" type="text" class="name username" v-model="username">
				</div>
				<div class="f2">
					<label for="psd" class="label2">密码</label>
					<input class="password" id="psd" type="password" v-model="pwd">
				</div>

				<button class="denglu" @tap="login_index" type="primary">登&nbsp;&nbsp;录</button>
		</div>
		<div class="bottom">
			<image src="../../static/login/logo_img2.png" mode="widthFix"></image>
		</div>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				textImgUrl:'',
				bgImg:'',
				apiUrl:[
					'https://weixin.zktop.com/jingzhang',  //京张
					'https://weixin.zktop.com/jingshen'   //京沈
				],
				dev:0,
				textImgUrlArr:[
					"../../static/login/jz_login.png",
					"../../static/login/js_login.png",
					"../../static/login/dongaohui_login.png"
				],
				bgImgUrl:[
					"../../static/login/jzhang_iphone_bg.jpg",
					"../../static/login/js_iphone_bg.jpg",
					"../../static/login/dongaohui_bg.jpg"
				],
				
				username:'',
				pwd:''
			};
		}, 
		onLoad: function (options) {       //options用于接收上个页面传递过来的参数
			this.dev = options.dev-1
			this.bgImg = this.bgImgUrl[options.dev-1]
			this.textImgUrl = this.textImgUrlArr[options.dev-1]
			//console.log(this.dev)
			wx.setNavigationBarTitle({
			  title: '登录'
			})
		},
		methods:{
			login_index(){
					let vm = this
					if (this.username.length <= 0) {
						uni.showToast({
							icon: 'none',
							title: '请输入用户名'
						});
						return;
					}
					if (this.pwd.length <= 0) {
						uni.showToast({
							icon: 'none',
							title: '请输入密码'
						});
						return;
					}
			
					uni.request({
						url:  vm.apiUrl[vm.dev] + '/user/login.shtml', // /zzcismp/base/getProjBaseInfoAll.shtml
						header: {
						  'content-type': 'application/json'
					    },
						data: {
							username: this.username,
							password: this.pwd
						},
						dataType: 'json',
						jsonp: "callback",
						success: (res) => {
							let list = res.data;
							console.log(res.data);
							if(list.status != 1){
								uni.showToast({
									icon: 'none',
									title: '用户名或密码错误'
								});
								return;
							}
			 
			                uni.showToast({
								icon: 'none',
								title: '登录成功'
							});
							uni.setStorage({
								key:'session_id',
								data:list['session_id']
							})
							
							uni.navigateTo({
								url: '../index/index'+'?porject='+vm.dev,
							});

						},
						fail: () => {
							uni.showToast({
								icon: 'none',
								title: '网络异常,请稍后重试',
								
							});
							
						}
			
					})
					uni.request({
						url: vm.apiUrl[vm.dev] + '/base/getProjBaseInfoAll.shtml',
						method: 'GET',
						data: {},
						dataType: 'json',
						jsonp: "callback",
						success: res => {
							console.log(res)
						},
						fail: () => {},
						complete: () => {}
					});
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
		font-size: 16px;
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
	.login_box{
		width: 64%;
		position: absolute;
		top:40%;
		left: 50%;
		transform: translate(-50%,-50%);
		z-index: 20;
	}
	.login_box image{
		width: 100%;
	}
	.f1,.f2{
		width: 100%;
		height: 38px;
		line-height: 38px;
		margin: 22px 0;
		border: 1px solid #666666;
		border-radius: 22px;
		display: flex;
		align-items: stretch;
		color: #333;
	}
	.label1,.label2{
		margin-left: 15px;
		display: inline-block;
		
	}
	.login_box input{
		padding-left: 2px;
		width: 70%;
		height: 100%;
		display: inline-block;
	}
	.denglu{
		height: 38px;
		line-height: 38px;
		border-radius: 19px;
		background:linear-gradient(#59f0ea,#43aea8);
		font-size: 16px;
		color: #FFFFFF;
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
