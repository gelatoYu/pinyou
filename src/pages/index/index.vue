<template>
  <div class="index-container">
    <!-- 搜索框 -->
    <div class="search-box">
      <input type="text" placeholder="搜索">
      <icon class="search-icon" type="search" size="12"></icon>
    </div>
    <!-- 轮播图 -->
    <div class="swiper-container">
      <swiper indicator-dots autoplay circular>
        <swiper-item v-for="item in swiperList" :key="item.image_src">
          <img mode="aspectFill" :src="item.image_src">
        </swiper-item>
      </swiper>
    </div>
    <!-- 分类按钮 -->
    <div class="category-container">
      <div class="item" v-for="item in categoryList" :key="item.image_src">
        <img :src="item.image_src" alt>
        <p>{{item.name}}</p>
      </div>
    </div>
    <!-- 楼层区域 -->
    <div class="floor-container">
      <div class="floor" v-for="item in floorList" :key="item.floor_title.image_src">
        <div class="top">
          <img :src="item.floor_title.image_src" alt>
          <h3>{{item.floor_title.name}}</h3>
        </div>
        <div class="bottom">
          <img :src="it.image_src" alt v-for="(it,i) in item.product_list">
        </div>
      </div>
    </div>
    <!-- 底部 -->
    <div class="bottom-line">
      <i class="iconfont icon-xiao"></i>
      <p>已经到底啦</p>
    </div>
    <!-- 回到顶部 -->
    <div class="back-top" v-show="isShow" @click="backTop">
      <i class="iconfont icon-jiantoushang"></i>
      <p>顶部</p>
    </div>
  </div>
</template>

<script>
import hxios from "../../utils/hxios.js";

export default {
  data() {
    return {
      swiperList: [],
      categoryList: [],
      floorList: [],
      isShow: false
    };
  },
  async created() {
    // //轮播图数据获取
    // let res = await hxios.get({
    //   url: "api/public/v1/home/swiperdata"
    // });
    // // console.log(res);
    // this.swiperList = res.data.message;

    // //分类按钮数据获取
    // let categoryRes = await hxios.get({
    //   url: "api/public/v1/home/catitems"
    // });
    // // console.log(categoryRes);
    // this.categoryList = categoryRes.data.message;

    // //楼层获取
    // let floorRes = await hxios.get({
    //   url: "api/public/v1/home/floordata"
    // });
    // console.log(floorRes);
    // this.floorList = floorRes.data.message;

    let p1 = hxios.get({
      url: "api/public/v1/home/swiperdata"
    });
    let p2 = hxios.get({
      url: "api/public/v1/home/catitems"
    });
    let p3 = hxios.get({
      url: "api/public/v1/home/floordata"
    });
    let res = await Promise.all([p1, p2, p3]);
    console.log(res);

    this.swiperList = res[0].data.message;
    this.categoryList = res[1].data.message;
    this.floorList = res[2].data.message;
  },
  onPageScroll(event) {
    if (event.scrollTop > 170) {
      this.isShow = true;
    } else {
      this.isShow = false;
    }
  },
  methods: {
    backTop() {
      wx.pageScrollTo({
        scrollTop: 0
      });
    }
  }
};
</script>

<style lang="scss">
$pinyou: #ff2d4a;
.index-container {
  padding-top: 100rpx;
  .search-box {
    z-index: 999;
    background-color: #ff2d4a;
    padding: 20rpx 16rpx;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    box-sizing: border-box;
    input {
      display: block;
      width: 100%;
      background-color: #fff;
      height: 60rpx;
      padding-left: 376rpx;
      font-size: 24rpx;
      border-radius: 10rpx;
      box-sizing: border-box;
    }
    .search-icon {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-70%, -50%);
    }
  }
  .swiper-container {
    swiper {
      height: 340rpx;
      swiper-item {
        img {
          display: block;
          width: 100%;
        }
      }
    }
  }
  .category-container {
    display: flex;
    // flex-wrap: wrap;
    padding: 29rpx;
    padding-top: 24rpx;
    .item {
      flex: 1;
      img {
        display: block;
        width: 128rpx;
        height: 128rpx;
        margin: 0 auto;
      }
      p {
        text-align: center;
        margin-top: 10rpx;
        font-size: 24rpx;
      }
    }
  }
  .floor-container {
    .floor {
      .top {
        padding-top: 30rpx;
        padding-bottom: 30rpx;
        padding-left: 15rpx;
        position: relative;
        height: 90rpx;
        box-sizing: border-box;
        img {
          position: absolute;
          height: 90rpx;
          left: 0;
          top: 0;
          display: block;
          width: 100%;
        }
        h3 {
          color: #ff7b94;
          position: absolute;
          left: 30rpx;
          top: 50%;
          transform: translateY(-50%);
        }
      }
      .bottom {
        padding: 20rpx 0 0 16rpx;
        overflow: hidden;
        img {
          display: block;
          width: 33.333%;
          float: left;
          width: 230rpx;
          height: 190rpx;
          margin-right: 10rpx;
          &:first-child {
            width: 230rpx;
            height: 390rpx;
          }
          &:nth-child(2) {
            margin-bottom: 10rpx;
          }
          &:nth-child(3) {
            margin-bottom: 10rpx;
          }
        }
      }
    }
  }
  .bottom-line {
    display: flex;
    justify-content: center;
    font-size: 24rpx;
    color: #999;
    padding: 20rpx 0;
  }
  .back-top {
    width: 90rpx;
    height: 90rpx;
    background-color: white;
    position: fixed;
    right: 15rpx;
    bottom: 15rpx;
    border-radius: 50%;
    z-index: 999;
    text-align: center;
    font-size: 26rpx;
  }
}
</style>
