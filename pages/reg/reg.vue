<template>
    <view class="content">
        <view class="input-group">
            <view class="input-row border">
                <text class="title">用户名：</text>
                <m-input type="text" focus clearable v-model="username" placeholder="请输入用户名"></m-input>
            </view>
            <view class="input-row border">
                <text class="title">密码：</text>
                <m-input type="password" displayable v-model="password" placeholder="请输入密码"></m-input>
            </view>
            <view class="input-row">
                <text class="title">邮箱：</text>
                <m-input type="text" clearable v-model="email" placeholder="请输入邮箱"></m-input>
            </view>
			<view class="input-row">
			    <text class="title">手机号：</text>
			    <m-input type="text" clearable v-model="mobile" placeholder="请输入手机号"></m-input>
			</view>
        </view>
        <view class="btn-row">
            <button type="primary" class="primary" @tap="register">注册</button>
        </view>
    </view>
</template>

<script>
    import service from '../../service.js'
    import mInput from '../../components/m-input.vue'
	import http from '../../components/utils/http.js'

    export default {
        components: {
            mInput
        },
        data() {
            return {
                username: '',
                password: '',
                email: '',
				mobile: ''
            }
        },
        methods: {
            register() {
                /**
                 * 客户端对账号信息进行一些必要的校验。
                 * 实际开发中，根据业务需要进行处理，这里仅做示例。
                 */
                if (this.username.length < 5) {
                    uni.showToast({
                        icon: 'none',
                        title: '账号最短为 5 个字符'
                    });
                    return;
                }
                if (this.password.length < 6) {
                    uni.showToast({
                        icon: 'none',
                        title: '密码最短为 6 个字符'
                    });
                    return;
                }
                if (this.email.length < 3 || !~this.email.indexOf('@')) {
                    uni.showToast({
                        icon: 'none',
                        title: '邮箱地址不合法'
                    });
                    return;
                }

                // const data = {
                //     account: this.account,
                //     password: this.password,
                //     email: this.email
                // }
                // service.addUser(data);
				let opts = {
					url: '/api/user/register',
					method: 'GET',
				};
				let param = {
					username: this.username,
					password: this.password,
					email: this.email,
					mobile: this.mobile
				};
				http.httpRequest(opts, param).then(res => {
					console.log(res.data)
					if(res.data.code == 1){
						 uni.showToast({
						    title: res.data.msg
						});
						setTimeout(()=>{
							uni.navigateBack({
							    delta: 1
							});
						},500)
					}else {
						uni.showToast({
							title: res.data.msg
						});
					}
				},error => {
					console.log(error)
				})
               
                
            }
        }
    }
</script>

<style>

</style>
