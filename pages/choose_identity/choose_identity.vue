<template>
	<view>
		<button type="primary" @click="enterprise()">企业端</button>
		<button type="primary" @click="hunter()">猎手端</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods: {
			enterprise () {
				uni.navigateTo({
					url: '/pages/index/index?type=3'
				});
			},
			hunter () {
				uni.navigateTo({
					url: '/pages/index/index?type=4'
				});
			},
		}
	}
</script>

<style>

</style>
