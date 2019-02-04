<template>
  <div class="home">
    <loadding :isLoadding = 'isLoadding' :loaddingText="'数据正在加载中。。。'"/>
    <div v-show="isHomeTabbar">
      <msgList :listData="datas" :scrollView='scrollView' :scrolltolower = 'scrolltolower' :onRefresh = 'onRefresh' :isShowMsg = 'true'
      :isCircleLoadding = 'isCircleLoadding' :stopHttp = 'stopHttp' :isSearchPage = 'false' :scrollTop = '0'/>
    </div>
    <div v-show="isMyTabbar">
      <myTabbar :scrollView='scrollView'/>
    </div>
    <wux-tabbar default-current="tab1" position='bottom' @change="changeTabbar">
        <wux-tabbar-item key="tab1" title="首页">
            <wux-icon wux-class="icon" type="ios-home" size="22" slot="icon-on" />
            <wux-icon wux-class="icon" type="ios-home" size="22" slot="icon-off" />
        </wux-tabbar-item>
        <!-- <wux-tabbar-item key="tab2" title="发现">
            <wux-icon wux-class="icon" type="ios-basketball" size="22" slot="icon-on" />
            <wux-icon wux-class="icon" type="ios-basketball" size="22" slot="icon-off" />
        </wux-tabbar-item> -->
        <wux-tabbar-item key="tab3" title="我的" id="wuxTabbarItem">
            <wux-icon wux-class="icon" type="ios-person" size="22" slot="icon-on"/>
            <wux-icon wux-class="icon" type="ios-person" size="22" slot="icon-off" />
        </wux-tabbar-item>
    </wux-tabbar>
</div>
</template>
<script>
import msgList from '@/components/msgList'
import loadding from '@/components/loadding'
import myTabbar from '@/components/myTabbar'
import { $stopWuxRefresher } from '../../../static/index.js'

export default {
  name: 'Home',
  data() {
    return {
      scrollView: 0,
      datas: [],
      isCircleLoadding: false,
      page: 0,
      stopHttp: false,
      isCloseBox: false,
      isHomeTabbar: true,
      isMyTabbar: false
    }
  },
  components: {
    msgList,
    loadding,
    myTabbar
  },
  methods: {
    requireDatas() {
      let newData = []
      setTimeout(()=> {
        this.page++
        this.datas = [
          {
            img: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3813794925,855224918&fm=26&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1146596355,1662249573&fm=26&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=4029951638,1644589634&fm=26&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3168701399,1765140883&fm=26&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=4236672645,228537459&fm=200&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2569952283,2386296470&fm=26&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2898135166,3129421746&fm=200&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=370406787,2865032899&fm=200&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
          {
            img: 'https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2241961014,2880285553&fm=26&gp=0.jpg',
            title: '海外市场总监',
            salary: '30K-45K',
            corporateName: '美团点评',
            address: '上海',
            addressArea: '世纪公园',
            yearsLimit: '3年以上',
            Education: '本科',
            Release: '11:10'
          },
        ]
        if(this.page > 1) {
          newData = [
            {
              img: 'https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1393128212,1038493965&fm=26&gp=0.jpg',
              title: '海外市场总监',
              salary: '30K-45K',
              corporateName: '美团点评',
              address: '上海',
              addressArea: '世纪公园',
              yearsLimit: '3年以上',
              Education: '本科',
              Release: '11:10'
            },
            {
              img: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=768433488,3208559730&fm=200&gp=0.jpg',
              title: '海外市场总监',
              salary: '30K-45K',
              corporateName: '美团点评',
              address: '上海',
              addressArea: '世纪公园',
              yearsLimit: '3年以上',
              Education: '本科',
              Release: '11:10'
            },
            {
              img: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3451923138,78858025&fm=200&gp=0.jpg',
              title: '海外市场总监',
              salary: '30K-45K',
              corporateName: '美团点评',
              address: '上海',
              addressArea: '世纪公园',
              yearsLimit: '3年以上',
              Education: '本科',
              Release: '11:10'
            },
            {
              img: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1127808616,1781056719&fm=26&gp=0.jpg',
              title: '海外市场总监',
              salary: '30K-45K',
              corporateName: '美团点评',
              address: '上海',
              addressArea: '世纪公园',
              yearsLimit: '3年以上',
              Education: '本科',
              Release: '11:10'
            },
            {
              img: 'https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3117597777,3227249676&fm=26&gp=0.jpg',
              title: '海外市场总监',
              salary: '30K-45K',
              corporateName: '美团点评',
              address: '上海',
              addressArea: '世纪公园',
              yearsLimit: '3年以上',
              Education: '本科',
              Release: '11:10'
            }
          ]
        }
        if(newData.length > 0)
        this.datas = this.datas.concat(newData)
        this.isCircleLoadding = false
        this.isLoadding = false
        if(this.page > 1) this.stopHttp = true
      }, 800)
    },
    changeTabbar(ev) {
      switch(ev.target.key) {
        case 'tab1':
          this.isMyTabbar = false
          this.isHomeTabbar = true
          break;
        case 'tab3':
          this.isHomeTabbar = false
          this.isMyTabbar = true
          break;
      }
    },
    getDomSize(data) {
      const query = wx.createSelectorQuery(), _this = this
      query.select(`#${data.id}`).boundingClientRect()
      query.exec(function (res) {
        _this.scrollView = res[0].top
      })
    },
    scrolltolower() {
      if(this.stopHttp) return false
      this.isCircleLoadding = true
      this.requireDatas()
      console.log(this.$http)
    },
    onRefresh() {
        this.page = 0
        this.stopHttp = false
        this.isCircleLoadding = false
        $stopWuxRefresher()
    },
    onSubscribe() {
      this.isCloseBox = true
    },
    closeBox() {
      this.isCloseBox = false
    }
  },
  mounted() {
    this.getDomSize({
      id: 'wuxTabbarItem'
    })
  },
  created() {
    this.isLoadding = true
    this.requireDatas()
    this.scrollView = wx.getSystemInfoSync().windowHeight
  }
}
</script>
<style>
  .home{
    width: 100%;
    height: 100%;
    background: #f1f1f1;
  }
</style>

/**
this.$fly.request({
     method:"post", //post/get 请求方式
     url:"/mms/country/queryValidZoneListForMallHome",
     body:{}
   }).then(res =>{
     console.log(res)
})
 */



