<!-- created by Zack 2023-0201 -->
<template>
	<view class="popup" v-if="show">
		<!-- notice -->
		<view class="notice">
			<view style="display: flex;margin: 10px;">
				<!-- your logo -->
				<image class="avatar small" src="/static/avatar-picker/img/notesbook.png"></image>
				<!-- your applet name -->
				<view class="applet">notesbook</view>
			</view>
			<view style="margin: 10px;color: #ffffff;" @tap="done">
				<text class="cuIcon-close"></text>
			</view>
		</view>
		<!-- container -->
		<view class="container">
			<swiper style="height: 100%;" acceleration :current="current" @animationfinish="tabChange" disable-touch>
				<swiper-item>
					<!-- user avatar -->
					<view class="item">
						<view class="left" style="color: red;">
							<!-- 	<view class="operations"></text></view> -->
						</view>
						<view class="center">
							<button open-type="chooseAvatar" @chooseavatar="onChooseAvatar">
								<image class="avatar chooseAvatar" style="background-color: darkgrey;"
									:src="choosedAvatar">
							</button>
						</view>
						</image>
						<view class="right cuIcon-pullright " :class="current==0?'cur':''" @tap="change">
							<!-- 	<view class="operations"></text></view> -->

						</view>
					</view>
				</swiper-item>
				<swiper-item>
					<!-- user nickName -->
					<view class="item">
						<view class="left cuIcon-pullleft" :class="current==1?'cur':''" @tap="change">
							<!-- 	<view class="operations"></text></view> -->
						</view>
						<view class="center">
							<input type="nickname" class="" auto-focus="true" placeholder="请输入昵称" @blur="chooseNickName"
								adjust-position="true" />
						</view>
						</image>
						<view class="right cuIcon-roundcheck " :class="nickname?'green':''" @tap="done">
							<!-- 	<view class="operations"></text></view> -->

						</view>
					</view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import {
		pathToBase64
	} from '@/static/avatar-picker/js/image.js'
	export default {
		name: 'avatar-picker',
		mounted() {
			console.log('picker was mounted')
		},
		props: {
			show: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				current: 0,
				choosedAvatar: '',
				nickname: ''
			}
		},
		methods: {
			tabChange(e) {
				this.current = e.detail.current
			},
			change(e) {
				this.current = this.current == 0 ? 1 : 0
			},
			chooseNickName(e) {
				this.nickname = e.detail.value;
			},
			onChooseAvatar(e) {
				let _this = this;
				pathToBase64(e.detail.avatarUrl).then(base64 => {
					this.choosedAvatar = base64;
				}).catch(error => {
					console.error(error)
				})
			},
			done(e) {
				let params = {
					"show": !this.show,
					"nickname": this.nickname,
					"avatar": this.choosedAvatar
				}
				this.$emit("showPopup", params)
			}
		}
	}
</script>

<style scoped>
	.popup {
		position: relative;
		width: 100vw;
		height: 30vh;
		position: fixed;
		bottom: 0;
		border-radius: 10px 10px 0 0;
		box-shadow: 0px 2px 4px 5px rgba(255, 252, 253, .1);
		z-index: 999;

	}

	/**
	 * 毛玻璃纹理图由 小程序notesbook提供
	 */
	.popup::before {
		content: '';
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 100%;
		border-radius: 10px 10px 0 0;
		background-image: url(@/static/avatar-picker/img/mbl.png);
		z-index: -1;
		backdrop-filter: blur(13.8px);
	}

	.notice {
		width: 100%;
		display: flex;
		justify-content: space-between;
		position: absolute;
		z-index: 1000;

	}


	.avatar {
		font-variant: small-caps;
		margin: 0;
		padding: 0;
		display: inline-flex;
		text-align: center;
		justify-content: center;
		align-items: center;
		color: #ffffff;
		white-space: nowrap;
		position: relative;
		width: 100%;
		height: 100%;
		font-size: 1em;
		background-size: cover;
		background-position: center;
		vertical-align: middle;
		border-radius: 50%;
	}

	.avatar.small {
		width: 48upx;
		height: 48upx;
	}

	.applet {
		margin-left: 10rpx;
		color: white;
		font-size: 0.9rem;
		font-weight: 800;
	}

	.container {
		width: 100%;
		height: 30vh;
		position: absolute;
	}

	.item {
		display: flex;
		justify-content: space-between;
		height: 100%;
		color: rgba(12, 12, 3, .1);
	}

	.chooseAvatar {
		height: 148upx;
		width: 148upx;
		border-radius: 50%;
		padding: 0px;

	}

	.left {
		flex: 1;
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		font-size: 1.5em;
	}

	.center {
		flex: 4;
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}

	.right {
		flex: 1;
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		font-size: 1.5em;

	}

	.operations {
		height: 50upx;
		width: 50upx;
		background-color: rgba(0, 0, 0, 0.2);
		border-radius: 50%;

	}

	.cur {
		color: rgba(12, 12, 3, .9);
	}

	.green {
		color: rgba(255, 255, 255, .6);
	}

	button {
		padding-left: 0px;
		padding-right: 0px;
		background-color: unset;
		border-radius: 50%;
	}

	button::after {
		height: 100%;
		border: none;
		color: unset;
		background-color: unset;
	}

	input {
		font-size: inherit;
		height: 128rpx;
		text-align: center;
		color: #000;
		outline: none;
		font-weight: 430;
		line-height: 1.6%;
		border-radius: 10px;
		background-color: rgba(0, 0, 0, 0.2);
	}
</style>
