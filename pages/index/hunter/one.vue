<template>
	<view style="padding-bottom: 500upx;">
		<view style="overflow: hidden;">
			<!-- <button type="primary" @click="$store.dispatch('menu_2')">2个菜单</button> -->
			<button type="primary" @click="$store.dispatch('menu_3')">3个菜单</button>
			<button type="primary" @click="$store.dispatch('menu_4')">4个菜单</button>
			123
			<!-- <button type="primary" @click="$store.dispatch('menu_5')">5个菜单</button> -->
		<!-- 	<button type="primary" @click="open_loading">显示loading</button>
			<button type="primary" @click="test_get()">测试GET</button>
			<button type="primary" @click="test_post()">测试POST</button> -->
		</view>
		<view v-if="hasLogin" class="hello">
		    <view class="title">
		        您好 {{userName}}，您已成功登录。
		    </view>
		    <view class="ul">
		        <view>这是 uni-app 带登录模板的示例App首页。</view>
		        <view>在 “我的” 中点击 “退出” 可以 “注销当前账户”</view>
		    </view>
		</view>
		<view v-if="!hasLogin" class="hello">
		    <view class="title">
		        您好 游客。
		    </view>
		    <view class="ul">
		        <view>这是 uni-app 带登录模板的示例App首页。</view>
		        <view>在 “我的” 中点击 “登录” 可以 “登录您的账户”</view>
		    </view>
		</view>

<!-- 		<view class="item" @click="get_detail(item.id)" v-for="(item, index) in list" :key="index">{{ item.title }}</view>
		<view class="des">数据来自 nodejs 中文社区 API</view> -->
	</view>
</template>
<script>
	import http from '../../../components/utils/http.js'
	import {
	    mapState
	} from 'vuex'
	export default {
		computed: mapState(['forcedLogin', 'hasLogin', 'userName']),
		data() {
			return {};
		},
		computed: {
			list() {
				return this.$store.state.list;
			}
		},
		methods: {
			open_loading() {
				this.$loading();
			},
			get_detail(id) {
				uni.navigateTo({
					url: '/pages/detail/detail?id=' + id
				});
			},
			test_get() {
				this.$ajax
					.get({
						url: '/admin/get_product_list',
						data: {
							a: 1
						}
					})
					.then(res => {
						this.$alert('状态码：' + res.code);
						console.log(res);
					});
			},
			test_post() {
				// 基本同GET
				this.$ajax
					.post({
						url: '/admin/get_product_list'
					})
					.then(res => {
						this.$alert(res.code);
						console.log(res);
					});
			}
		},
		onLoad() {
		    if (!this.hasLogin) {
		        uni.showModal({
		            title: '未登录',
		            content: '您未登录，需要登录后才能继续',
		            /**
		             * 如果需要强制登录，不显示取消按钮
		             */
		            showCancel: !this.forcedLogin,
		            success: (res) => {
		                if (res.confirm) {
							/**
							 * 如果需要强制登录，使用reLaunch方式
							 */
		                    if (this.forcedLogin) {
		                        uni.reLaunch({
		                            url: '../login/login'
		                        });
		                    } else {
		                        uni.navigateTo({
		                            url: '../login/login'
		                        });
		                    }
		                }
		            }
		        });
		    }
		}
	};
</script>

<style>
.item {
	font-size: 28upx;
	line-height: 60upx;
	height: 60upx;
	border-bottom: 2upx solid #f1f1f1;
	padding-left: 30upx;
	padding-right: 30upx;
	color: #888;
	text-align: left;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.des {
	text-align: center;
	padding: 30upx;
	margin-top: 100upx;
	font-size: 30upx;
	color: #888888;
}
button {
	width: 330upx;
	float: left;
	margin-left: 30upx;
	margin-top: 30upx;
	padding: 10upx 20upx;
	font-size: 32upx;
}
</style>
