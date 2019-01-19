<template>
    <div class="msgList">
        <wux-refresher id="wux-refresher" @refresh="onRefresh" @pulling="onPulling">
            <scroll-view  :style="{'height': scrollView + 'px', paddingTop: scrollTop}" :scroll-y="true" @scrolltolower="scrolltolower">
                <div :class="[isActivedS ? 'activedS' : 'recruitmentSubscription']" @click="subscribe" v-show="isShowMsg">订阅爱招聘</div>
                <div v-for='(item, index) in listData' :key="index" @click="goDetails(item)"
                :class="[index == listData.length - 1 ? 'listDataLast' : 'listData']">
                    <div class="list">
                        <div class="placeholderLeft" :style="{backgroundImage: 'url(' + item.img + ')'}"></div>
                        <div class="placeholderMiddle">
                            <div class="placeholderRigth">
                                <div>{{item.title}}</div>
                                <div>{{item.salary}}</div>
                            </div>
                            <div>{{item.address}}|{{item.addressArea}}|{{item.yearsLimit}}|{{item.Education}}</div>
                        </div>
                    </div>
                    <div class="listMark">{{item.Release}} @{{item.corporateName}}</div>
                </div>
                <div class="circleLoadding" v-show="isCircleLoadding"></div>
                <div v-show="stopHttp">
                    <wux-divider dashed position="center" text="全部加载完成"/>
                </div>
            </scroll-view>
        </wux-refresher>
    </div>
</template>

<script>
export default {
  name: 'msgList',
  props: ['listData', 'scrollView','isCircleLoadding','stopHttp','isSearchPage','scrollTop','isShowMsg'
  ,'scrolltolower', 'onRefresh'
],
  data() {
      return {
          isActivedS: false
      }
  },
  methods: {
      onFocus() {
          const url = '../search/main'
          wx.navigateTo({ url })
      },
      goDetails(items) {
          const url = '../details/main'
          let obj = {
            title:'',
            salary: '',
            address: '',
            addressArea: '',
            yearsLimit: '',
            Education: ''
          }
          for(let [index, item] of Object.entries(obj)) {
              obj = Object.assign(obj, {[index]: items[index]})
          }
          let parames = JSON.stringify(obj)
          wx.navigateTo({ url: `${url}?parames=${parames}`})
      },
      onPulling() {
        console.log('onPulling')
    },
    subscribe() {
        this.isActivedS = !this.isActivedS
        this.isActivedS ?
        wx.showToast({
            title: '感谢您的订阅',
            icon: 'success',
            duration: 2000//持续的时间
        })
        : wx.showToast({
            title: '取消订阅成功',
            icon: 'success',
            duration: 2000//持续的时间
        })
    }
  }
}
</script>

<style>
    .circleLoadding{
        margin: 30rpx 50%;
        width: 40rpx;
        height: 40rpx;
        border: 1rpx white solid;
        border-left-color: #ff5500;
        border-right-color:#0c80fe;
        border-radius: 100%;
        animation: loading1 1s infinite linear;
    }
    @keyframes loading1{
        from{transform: rotate(0deg)}to{transform: rotate(360deg)}
    }
    .listData{
        border: 1rpx solid #c6c5ca;
        margin-bottom: 20rpx;
    }
    .listDataLast{
        border: 1rpx solid #c6c5ca;
        margin-bottom: 0;
    }
    ::-webkit-scrollbar{
        width: 0;
        height: 0;
        color: transparent;
    }
    .msgList{
        width: 90%;
        margin: 0 auto;
    }
    .recruitmentSubscription{
        width: 300rpx;
        height: 80rpx;
        border: 1rpx solid #c6c5ca;
        background: #fff;
        border-radius: 80rpx;
        line-height: 80rpx;
        text-align: center;
        margin: 0 auto 70rpx auto;
        font-size: 15px !important;
        color: #000;
    }
    .activedS{
        width: 300rpx;
        height: 80rpx;
        border: 1rpx solid #c6c5ca;
        border-radius: 80rpx;
        line-height: 80rpx;
        text-align: center;
        margin: 0 auto 70rpx auto;
        background: #51C83D;
        font-size: 15px !important;
        color: #fff;
    }
    .placeholderLeft{
        width: 150rpx;
        height: 150rpx;
        background-size: 100% 100%;
        margin: 20rpx 0 20rpx 20rpx;
    }
    .list{
        width: 100%;
        display: flex;
        background: #fff;
        height: 200rpx;
    }
    .placeholderMiddle, .placeholderRigth{
        font-size: 15px;
    }
    .placeholderMiddle{
        display: flex;
        justify-content: space-between;
        flex-direction: column;
        margin: 20rpx 0 20rpx 20rpx;
    }
    .listMark{
        font-size: 12px;
        color: #bbb;
        background: #fafafa;
        padding: 4rpx 20rpx;
    }
</style>