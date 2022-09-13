<template>
  <view class="page">
    <view class="headerLogo">GreenBanker</view>
    <view>
      <Xsuu-swiper
        :swiperItems="swiperItems"
        class="swiper"
		@click="navigate"
      ></Xsuu-swiper>
    </view>
    <view class="btnBox">
      <view class="bigBtn">
        <image src="../../static/icon/scan.svg"></image>
        点击扫码，即可参与环保</view
      >
    </view>
    <view class="articleBox">
        <view></view>
        <view></view>
        <view></view>
        <view></view>
    </view>
  </view>
</template>

<script>
import XsuuSwiper from "../../components/Xss-swiper/Xsuu-swiper.vue";
export default {
  // 注册组件
  components: { XsuuSwiper },
  data() {
    return {
      swiperItems: [
        {
          img: "https://img-blog.csdnimg.cn/47f71924f457432cab9ef11c582bbe73.png",
          title: "小测试",
          Subtitle: "你的环保型人格是什么",
          tip: "限时",
          url: "../questionnaire/questionnaire.vue",
        },
        {
          img: "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fs1.xchuxing.com%2Fxchuxing%2Fforum%2F201607%2F27%2F185524zj7wog6qizk9o90k.jpg&refer=http%3A%2F%2Fs1.xchuxing.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1619914861&t=4c64a4a5cec709f9d03507b793546646",
          title: "包月低至9.9元",
          Subtitle: "立享受充电礼包！",
          tip: "推荐",
          url: "111",
        },
        {
          img: "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_match%2F0%2F11780621658%2F0.jpg&refer=http%3A%2F%2Finews.gtimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1619914935&t=7d98cfe6b5a2634598fc7bda871aa7c9",
          title: "进口儿童座椅",
          Subtitle: "￥698.99",
          tip: "进口",
          url: "111",
        },
        {
          img: "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fstc.zjol.com.cn%2Fg1%2FM000E11CggSDVi-zTuAT1Y3AAB2NSzPgKI097.jpg%3Fwidth%3D576%26height%3D340&refer=http%3A%2F%2Fstc.zjol.com.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1619914972&t=9cc0a578d4818d87c43f1fe839010096",
          title: "品牌T恤",
          Subtitle: "￥22.99",
          tip: "nike",
          url: "111",
        },
      ],
    };
  },
  onLoad() {},
  methods: {
	  navigate(){
		  uni.navigateTo({url: '',fail:(err)=>{
		  	console.log(err)
		  }})
	  }
  },
};
</script>
<style scoped lang="scss">
.page {
  height: 400rpx;
  background: #56b78a;
  background-size: 120% auto;
  background-position: center;
  border-bottom-left-radius: 30%;
  border-bottom-right-radius: 30%;
}
.header {
  width: 100%;
  display: flex;
  justify-content: center;
}
.swiper {
  padding-top: 90rpx;
  margin: 0;
}
.headerLogo {
  color: white;
  font-size: 35rpx;
  font-weight: bold;
  padding: 10rpx 0 0 20rpx;
}
.bigBtn {
  width: 85%;
  background-color: #56b78a;
  height: 60rpx;
  color: white;
  font-size: 30rpx;
  line-height: 30rpx;
  font-weight: bold;
  padding: 20rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 1000rpx;
  margin-top: 50rpx;
  box-shadow: 0 0 20rpx #8b8b8b;
  image {
    width: 50rpx;
    height: 50rpx;
    margin-right: 20rpx;
  }
}

.btnBox {
  display: flex;
  justify-content: center;
}
.articleBox{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 25rpx;
  $articleWidth: 220rpx;
  view{
    width: $articleWidth;
    height: $articleWidth/3*4;
    background-color: green;
    border-radius: 20rpx;
    margin-top: 25rpx;
  }
}
</style>