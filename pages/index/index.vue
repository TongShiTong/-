<template>
	<view class="content">
		<homePage v-if="page_code=='home'"></homePage>
		<pageTwo v-if="page_code=='publish'"></pageTwo>
		<pageThree v-if="page_code=='my'"></pageThree>
		<one v-if="page_code=='one'"></one>
		<two v-if="page_code=='two'"></two>
		<three v-if="page_code=='three'"></three>
		<four v-if="page_code=='four'"></four>
		<fr-loading></fr-loading>
		<footerNav></footerNav>
		<!-- <button type="primary" @click="$store.dispatch('menu_3')">3个菜单</button>
		<button type="primary" @click="hunter()">4个菜单</button> -->
	</view>
</template>

<script>
	import homePage from "./pages/home_page.vue";
	import pageTwo from "./pages/page_two.vue";
	import pageThree from "./pages/page_three.vue";
	import footerNav from "../../components/footer/footer_nav.vue";
	import one from "./hunter/one.vue";
	import two from "./hunter/two.vue";
	import three from "./hunter/three.vue";
	import four from "./hunter/four.vue"
	export default {
		data() {
			return {}
		},
		components: {
			homePage,
			pageTwo,
			pageThree,
			footerNav,
			one,
			two,
			three,
			four
		},
		
		computed: {
			page_code() {
				return this.$store.state.footer_store.footer_nav[this.$store.state.footer_store.now_page_index].name_code;
			}
		},
		onLoad(e) {
			console.log(e)
			if(e.type== 4) {
				console.log('123')
				this.hunter()
			}
			console.log('index onload')
						this.$store.dispatch('get_data')
		},
		methods: {
			open_loading() {
				this.$loading()
			},
			hunter () {
				this.$store.dispatch('menu_4')
			}
		}
		
	}
</script>

<style>
	 
	.content {
		text-align: center;
		padding-bottom: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
