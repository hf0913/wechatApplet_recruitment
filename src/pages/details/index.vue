<template>
    <div class="details">
        <div class="position">{{shareDatas.title}}</div>
        <div class="welfare">
            <span class="salary">{{shareDatas.salary}}/</span>
            <span class="Work place">{{shareDatas.address + shareDatas.addressArea}}/</span>
            <span class="yearsLimit">{{shareDatas.yearsLimit}}/</span>
            <span class="education">{{shareDatas.Education}}</span>
        </div>
        <div class="mark">
            <span>职位诱惑：</span>
            <span>领导人nice</span>
        </div>

        <div style="margin: 40rpx 0 20rpx 0;">
            <wux-row>
                <wux-col span="10">
                    <div class="corporateName">爱乐奇</div>
                    <div class="corporateDatas">
                        <span>D轮及以上/</span>
                        <span>500-2000人/</span>
                        <span>移动互联网</span>
                    </div>
                </wux-col>
                <wux-col span="2">
                    <div class="placeholderLeft" :style="{backgroundImage: 'url(' + 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2517214011,1791773981&fm=26&gp=0.jpg'+ ')'}"></div>
                </wux-col>
            </wux-row>
        </div>
        
        <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
            <block v-for="(item, index) in images" :key="index">
                <swiper-item>
                    <image :src="item.url" class="slide-image" mode="aspectFill"/>
                </swiper-item>
            </block>
        </swiper> 

        <div class="companyProfile">公司简介</div>
        <div class="content">
            浙江百慕生物科技有限公司隶属浙江丽珀集团，成立于2011年3月，注册资本1000万元，是一家从事海洋生物开发销售的公司，主要从事保健品（海参）产品的销售。
旗下的优参堂海参品牌源自于卢炜翎先生创立的优参号参堂，经过一百多年的发展，现已成为最具规模化，现代化，专业化的海参加工生产企业之一。
        </div>
        <div class="jobDescription">职位描述</div>
        <div class="jobContent">
            1、使用React Native和Reactjs进行移动应用研发； 2、利用HTML5相关技术开发移动平台的WEB前端； 3、封装React Native原生组件，并Android与IOS客户端集成 4、redux相关工作流设计管理； 5、持续改进移动APP用户体验，性能、安全性、稳定性和可扩展性； 6、及时发现和提出问题，并能提出和实践可行性解决方案。 7、完成软件项目的详细设计，手册及单元测试文档的编制 8、负责完成代码的编写，项目集成，性能优化及技术支持 
        </div>
        <div class="subscribe" @click="subscribe">
            <span>->点我订阅该公司</span>
        </div>
        <wux-floating-button :position="position" :buttons="buttons" />
    </div>
</template>

<script>
const icon = "https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=130694900,417780414&fm=26&gp=0.jpg"
export default {
  name: 'details',
  props: {
  },
  data() {
    return {
      indicatorDots: true,
      autoplay: true,
      interval: 3000,
      duration: 1000,
      isShowBtn: true,
      shareDatas: {
        title:'',
        salary: '',
        address: '',
        addressArea: '',
        yearsLimit: '',
        Education: ''
      },
      images: [
        {
          url:
            "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2174623688,558265997&fm=26&gp=0.jpg"
        },
        {
          url:
            "https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=900392715,2167355354&fm=26&gp=0.jpg"
        },
        {
          url:
            "https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=3934866728,3376555721&fm=26&gp=0.jpg"
        }
      ],
      buttons: [
            {
                openType: 'share',
                label: '微信分享',
                icon,
            }
        ],
      position: 'bottomRight',
    }
  },
  mounted() {
    if(this.$root.$mp.query && 'parames' in this.$root.$mp.query) {
        this.shareDatas = JSON.parse(this.$root.$mp.query.parames)
    }
    

    if(this.$root.$mp.query && 'share' in this.$root.$mp.query)
    this.shareDatas = JSON.parse(this.$root.$mp.query.share)
  },
  methods: {
      subscribe() {
          wx.showToast({
            title: '感谢您的订阅',
            icon: 'success',
            duration: 2000//持续的时间
        })
      }
  },
  onShareAppMessage: (res) => {
    if (res.from === 'button') {
      console.log("来自页面内转发按钮");
      console.log(res.target);
    }
    else {
      console.log("来自右上角转发菜单")
    }
    let parames = JSON.stringify(this.shareDatas)
    return {
      title: '爱招聘',
      path: '/pages/details/main?share=parames',
      success: (res) => {
        console.log("转发成功", res);
      },
      fail: (res) => {
        console.log("转发失败", res);
      }
    }
  }
};
</script>

<style scoped>
.details{
    position: relative;
    width: 95%;
    margin: 0 auto;
    padding-bottom: 50rpx;
}
.swiper {
  height: 376rpx !important;
}
image {
  height: 100%;
  width: 100%;
}
.welfare{
    margin: 20rpx 0 10rpx 0;
    font-size: 13px;
}
.salary{
    color: red;
}
.mark{
    font-size: 13px;
    color: #999;
}
.position, .corporateName, .companyProfile, .jobDescription{
    font-size: 18px;
}
.corporateName, .companyProfile, .jobDescription{
    margin-top: 10rpx;
}
.corporateDatas,.content, .jobContent{
    font-size: 13px;
    margin-top: 20rpx;
}
.placeholderLeft{
    margin-left: 11rpx;
    width: 110rpx;
    height: 110rpx;
    background-size: 100% 100%;
}
.subscribe {
    margin-top: 20rpx;
    color: red;
}
</style>

