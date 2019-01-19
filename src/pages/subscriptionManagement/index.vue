<template>
    <div class="subscribeBox" :style="{height:boxHeight+'px'}">
        <wux-cell title="爱招聘更新推送" style="font-size: 15px">
            <wux-switch name="b" slot="footer" :value="value" @change="onChange" />
        </wux-cell>
        <div class="content">您还可以针对性订阅如下招聘信息类哦</div>
        <div class="box">
            <ul>
                <li v-for="(item,index) in tab" :key="index" @click="changeStyle(index)" 
                :class="[index === tabIndex[index] ? 'activedClass' : '']">{{item}}</li>
            </ul>
        </div>
    </div>
</template>
<script>
export default {
    name: 'subscribeBox',
    data() {
        return {
            tab: ['实习', '校招', '社招', '公司', '其他'],
            tabIndex: [-9, -9, -9, -9, -9],
            boxHeight: 0,
            value: false
        }
    },
    props: {
    },
    methods: {
        changeStyle(index) {
            if(this.tabIndex[index] == '-9'){
                this.tabIndex.splice(index, 1, index)
                wx.showToast({
                    title: '订阅成功',
                    icon: 'success',
                    duration: 1000//持续的时间
                })
            }
            else {
                this.tabIndex.splice(index, 1, -9)
                wx.showToast({
                    title: '取消成功',
                    icon: 'success',
                    duration: 2000//持续的时间
                })
            }
        },
        onChange() {
          this.value = !this.value
        }
    },
    mounted() {
        this.boxHeight = wx.getSystemInfoSync().windowHeight
    },
}
</script>
<style>
    .subscribeBox{
        width: 100%;
        height: 100%;
        background: #f1f1f1;
    }
    li {
        width: 300rpx;
        height: 80rpx;
        border: 1rpx solid #c6c5ca;
        background: #fff;
        border-radius: 80rpx;
        line-height: 80rpx;
        text-align: center;
        margin: 0 auto 70rpx auto;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .activedClass{
        background: #51C83D;
    }
    li:nth-of-type(1){
        margin-top: 50rpx;
    }
    .content{
        font-size: 15px;
        margin: 20rpx 20rpx;
        color: red;
    }
</style>


