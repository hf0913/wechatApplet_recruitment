<template>
  <div style="background:#fafafa">
    <div class="searchBox" :style="{height: searchBoxH + 'px'}">
        <wux-row style="border-bottom: 1px solid #fafafa" id="searchBar">
            <wux-col span="8">
                <input type = 'text' v-model="value" placeholder="请输入查询内容" @input= 'inputValue'/>
                <span class="close" @click="clearContet" v-show="isClearContet">X</span>
            </wux-col>
            <wux-col span="2">
                <div class="search" @click="search">搜索</div>
            </wux-col>
            <wux-col span="2">
                <wux-filterbar :items="items" style="heigth: 10rpx;"/>
            </wux-col>
        </wux-row>
    </div>
    <div :style="{background: '#fff'}" v-show="isShow">
        <msgList :listData="datas" :scrollView='scrollView' :scrolltolower = 'scrolltolower'  :onRefresh = 'onRefresh' :isShowMsg = 'false'
        :isCircleLoadding = 'isCircleLoadding' :stopHttp = 'stopHttp' :isSearchPage = 'true' :scrollTop='scrollTop'/>
    </div>
  </div>
</template>
<script>
import msgList from '@/components/msgList'
import { $stopWuxRefresher } from '../../../static/index.js'
export default {
    name: 'search',
    data() {
        return {
            scrollView: 0,
            datas: [],
            isCircleLoadding: false,
            stopHttp: false,
            isShow: false,
            isClearContet: false,
            value: '',
            scrollTop: 30,
            searchBoxH: 35,
            items: [
                {
                type: 'filter',
                label: '筛选',
                value: 'filter',
                children: [{
                        type: 'radio',
                        label: '请选择你需要查询的招聘类别（单选）',
                        value: 'language',
                        children: [{
                                label: '实习',
                                value: 'shixi',
                            },
                            {
                                label: '校招',
                                value: 'xiaozhao',
                            },
                            {
                                label: '社招',
                                value: 'shezhao',
                            },
                            {
                                label: '其他',
                                value: 'others',
                            }]
                    }]
                }]
        }
    },
    methods: {
        getDomSize(data) {
            const query = wx.createSelectorQuery(), _this = this,windowHeight = wx.getSystemInfoSync().windowHeight 
            query.select(`#${data.id}`).boundingClientRect()
            query.exec(function (res) {
                _this.scrollView = windowHeight - res[0].height
                _this.searchBoxH = res[0].height - 2
                _this.scrollTop = res[0].height + 2 + 'px'
            })
        },
        scrolltolower() {
            if(this.stopHttp) return false
            this.isCircleLoadding = true
            console.log(this.$http)
        },
        onRefresh() {
            $stopWuxRefresher()
        },
        clearContet() {
            this.value = ''
            this.isClearContet = false
        },
        inputValue(ev) {
            this.value = ev.target.value + ''
            this.value.length > 0 ? this.isClearContet = true : this.isClearContet = false
        },
        search() {
            this.datas = [
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
          this.stopHttp = true
          this.isShow = true
        }
    },
    mounted() {
        this.datas = []
        this.stopHttp = false
        this.isCircleLoadding = false,
        this.isShow = false
        this.getDomSize({
            id: 'searchBar'
        })
    },
    components: {
        msgList
    }
}
</script>
<style>
    .search{
        background: #fafafa;
        line-height: 70rpx;
        color: #000;
        text-align: center;
    }
    input[type=text]{
    margin: 0 0 0 10rpx !important;
    font-size: 13px;
    height: 70rpx;
    width: 490rpx;
    padding: 7rpx 8rpx;
    outline: none;
    color: #333;
    background-color: #fff;
    background-repeat: no-repeat;
    background-position: right center;
    border: 1px solid #ccc;
    border-radius: 3px;
    box-shadow: inset 0 1rpx 2rpx rgba(0,0,0,0.075);
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    transition: all 0.15s ease-in;
    -webkit-transition: all 0.15s ease-in 0;
    vertical-align: middle;
  }
  input[type=text]:focus{
    outline: none;
    border-color: #51a7e8;
    box-shadow: inset 0 1px 2px rgba(0,0,0,.075), 0 0 5px rgba(81,167,232,.5);
  }
  .close{
      position: absolute;
      top: 0;
      right: 0;
      padding:20rpx;
      font-size: 14px;
      color: red;
      z-index: 999
  }
  .searchBox{
      width: 100%;
      position: absolute;
      top:0;
      left: 0;
      overflow: hidden;
      background: #fafafa;
  }
</style>


