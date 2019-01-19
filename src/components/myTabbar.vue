<template>
    <div :style="{height: scrollView+'px'}">
        <button class="recruitmentSubscription" open-type="getUserInfo"
    @getuserinfo="re_getUserInfo" v-if="isShow">微信关联</button>
        <div class="userInfo">
            <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" @load="onLoad"/>
            <div class="userinfo-nickname">
                <card :text="userInfo.nickName"></card>
            </div>
        </div>
        <div class="subscriptionManagement" v-for="(item, index) in list" :key="index" @click="onClick(index)">
            <span class="subscriptionManagementContent">{{item}}</span>
        </div>
    </div>
</template>
<script>
import card from '@/components/card'
export default {
    name: 'myTabbar',
    props: {
        scrollView: {
            type: Number,
            required: true
        }
    },
    data(){
        return {
            list: ['订阅管理', '搜索招聘'],
            userInfo: {},
            isShow: true
        }
    },
    components: {
        card
    },
    methods: {
        re_getUserInfo(ev) {
            this.isShow = false
            const userInfo = ev.mp.detail.userInfo
            this.userInfo = {
                avatarUrl: userInfo.avatarUrl,
                city: userInfo.city,
                gender: userInfo.gender == 1 ? '男' : '女',
                nickName: userInfo.nickName,
                province: userInfo.province
            }
            wx.setStorageSync('userInfo', this.userInfo)
        },
        onLoad(){
            this.isShow = false
        },
        onClick(index) {
            let url = ''
            switch(index) {
                case 0:
                  url = '../subscriptionManagement/main'
                  wx.navigateTo({ url })
                  break;
                case 1:
                  url = '../search/main'
                  wx.navigateTo({ url })
                  break;
            }

        }
    },
    mounted() {
        const userInfo = wx.getStorageSync('userInfo')
        if(userInfo && 'avatarUrl' in userInfo && userInfo.avatarUrl !== '') {
            this.userInfo = userInfo
        }
    }
}
</script>
<style>
    .recruitmentSubscription{
        width: 300rpx;
        height: 80rpx;
        border: 1rpx solid #c6c5ca;
        background: #fff;
        border-radius: 80rpx;
        line-height: 80rpx;
        text-align: center;
        margin: 0 auto 70rpx auto;
        font-size: 15px;
    }
    .subscriptionManagement{
        width: 90%;
        height: 100rpx;
        background: #fff;
        text-align: left;
        line-height: 100rpx;
        border: 1rpx solid #c6c5ca;
        margin: 0 auto;
        font-size: 15px;
        margin-bottom: 20rpx;
    }
    .subscriptionManagementContent{
        margin-left: 30rpx;
    }
    .userinfo-avatar {
        width: 128rpx;
        height: 128rpx;
        margin: 20rpx;
        border-radius: 50%;
    }
    .userinfo-nickname {
        color: #aaa;
    }
    .userInfo{
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto;
        flex-direction: column;
    }
</style>


