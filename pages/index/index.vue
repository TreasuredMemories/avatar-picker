<template>
	<view class="back">
		<view class="padding" style="top: 10vh;position: absolute;width: 100%;">
			<button class="cu-btn block  text-bold bg-cyan light  lg" @click="authorize" >
				<text class="cuIcon-weixin " >授权登录</text></button>
				
		</view>
		<view v-if="nickName" style="width: 100%;height: 100%;">
			<text class="cuIcon-roundcheckfill text-green"></text>
		</view>
		<avatarpicker :show="show" @showPopup="showPopup"></avatarpicker>
	</view>
</template>

<script>
	import avatarpicker from '@/components/avatar-picker/avatar-picker.vue'
	export default {
		components:{
			avatarpicker
		},
		data() {
			return {
				show: false,
				nickName: '',
				avatar: ''
			}
		},
		onLoad() {
			
		},
		methods: {
			showPopup(e){
				console.log("收到头像和昵称：",e)
				this.show = e.show,
				this.nickName = e.nickName,
				this.avatar = e.avatar
				
			},
			authorize(){
				this.show=true
			}
		}
	}
</script>

<style>
	.back{
		height: 100vh;
		width: 100vh;
		background-image: url(https://c-ssl.dtstatic.com/uploads/item/202005/03/20200503123406_czCjJ.thumb.1000_0.jpeg);
		background-position: 0;
		background-repeat: no-repeat;
		background-size: cover;
	}
	button {
		padding-left: 0px;
		padding-right: 0px;
		background-color: unset;
		border-radius: unset;
	}
	
	button::after {
		height: 100%;
		border: none;
		color: unset;
		background-color: unset;
	}
</style>
