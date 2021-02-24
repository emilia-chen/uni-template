<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {
        console.log('this')
		},
        async onShow() {
            //async+await+Promise 让<if判断>在<getWeatherList返回结果后>执行
            let flag = await this.getWeatherList();
            if(flag){
                this.$tools.msg('已在控制台成功获取天气！')
            }else{
                this.$tools.msg('获取天气失败！')
            }
        },
		methods: {
            //获取天气（随便网上找的接口 可能会失效
            getWeatherList(page) {
                return new Promise((resolve, reject) => {
                    this.$api('test', {}).then(res => {
                        console.log('getWeatherList', res);
                        resolve(true);
                    }).catch((e)=>{
                        resolve(false);
                        // console.log(e);
                    });
                })
            
            },
		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
