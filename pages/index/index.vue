<template>
    <view class="container">       
        <view class="button-sp-area">
            <button type="primary" @click="getTrending()">{{status}}</button>
            <button type="primary" @click="toAnother()" plain="true">跳转界面</button>
			<view v-for="item in result">{{item.name}}</view>
        </view>	
    </view>
</template>

<script>
    export default {
        data() {
            return {
                status: '开始请求',
				result:[]
            }
        },
		onLoad(){

		},
        methods: {
            toAnother() {
                uni.navigateTo({
                    url: '/pages/another/another'
                })
            },
            getTrending() {
                uni.request({
                    url: 'https://github-trending-api.now.sh/repositories',
                    data: {
						since:'daily'
					},
                    success: (res) => {
                        this.status = '请求成功';
						this.result = res.data;
                    },
                    fail: (err) => {
                        
                    }
                });
            },
        }
    }
</script>

<style>
    .container {
        padding: 60px 0;
        font-size: 14px;
        line-height: 24px;
    }
    .button-sp-area {
        margin: 30rpx auto;
        width: 60%;
    }

    .button-sp-area button {
        width: 300rpx;
        margin-top: 20rpx;
        font-size: 14px;
    }
</style>
