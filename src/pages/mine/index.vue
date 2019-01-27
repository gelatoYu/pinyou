<template>
  <div class="mine-container">
    <div class="header">
      <div class="userIcon">
        <i class="iconfont icon-shezhi"></i>
        <button class="icon" open-type="getUserInfo" @getuserinfo="getUserInfo">
          <img :src="iconUrl" alt>
        </button>
        <i class="iconfont icon-xiaoxi"></i>
      </div>
      <div class="userInfo">
        <p>{{nickName}}</p>
      </div>
    </div>
    <div class="bottom">
      <!-- 收藏 -->
      <div class="history-box">
        <div class="item">
          <p>0</p>
          <p>收藏的店铺</p>
        </div>
        <div class="item">
          <p>0</p>
          <p>收藏的商品</p>
        </div>
        <div class="item">
          <p>0</p>
          <p>关注的商品</p>
        </div>
        <div class="item">
          <p>0</p>
          <p>我的足迹</p>
        </div>
      </div>
      <!-- 我的订单 -->
      <div class="order">
        <div class="title">我的订单</div>
        <div class="order-items">
          <div class="item">
            <i class="iconfont icon-daifukuan"></i>
            <p>待付款</p>
          </div>
          <div class="item">
            <i class="iconfont icon-daishouhuo"></i>
            <p>待收货</p>
          </div>
          <div class="item">
            <i class="iconfont icon-tuikuan"></i>
            <p>退款/退货</p>
          </div>
          <div class="item">
            <i class="iconfont icon-dingdan"></i>
            <p>全部订单</p>
          </div>
        </div>
      </div>
      <!-- 选项区域 -->
      <div class="options">
        <!-- 收货地址 -->
        <div class="option" @click="getAddress">
          <p>收货地址管理</p>
          <i class="iconfont icon-jiantouyou"></i>
        </div>
        <div class="option" @click="callService">
          <p>练习客服</p>
          <i>400-618-4000</i>
        </div>
        <div class="option">
          <p>意见反馈</p>
          <i class="iconfont icon-jiantouyou"></i>
        </div>
        <div class="option">
          <p>关于我们</p>
          <i class="iconfont icon-jiantouyou"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "../../utils/hxios.js";
export default {
  data() {
    return {
      iconUrl: "",
      nickName: "登录/注册"
    };
  },
  methods: {
    getUserInfo(event) {
      console.log(event);
      this.iconUrl = event.mp.detail.userInfo.avatarUrl;
      this.nickName = event.mp.detail.userInfo.nickName;
    },
    getAddress(){
      wx.chooseAddress({
        success: function(res) {
          console.log(res.userName);
          console.log(res.postalCode);
          console.log(res.provinceName);
          console.log(res.cityName);
          console.log(res.countyName);
          console.log(res.detailInfo);
          console.log(res.nationalCode);
          console.log(res.telNumber);
        }
      });
    },
    callService(){
      wx.makePhoneCall({ phoneNumber: '13631228421' });
    }
  }
};
</script>

<style lang="scss">
$pinyou: #ff2d4a;
page {
  background-color: #eee;
}
.mine-container {
  .header {
    background-color: $pinyou;
    width: 100%;
    height: 430rpx;
    padding-top: 120rpx;
    box-sizing: border-box;
    .userIcon {
      display: flex;
      justify-content: center;
      align-items: center;
      i {
        color: white;
      }
      .icon {
        width: 130rpx;
        height: 130rpx;
        border-radius: 50%;
        overflow: hidden;
        border: 5rpx solid white;
        margin: 0 65rpx;
        padding: 0;
        img {
          width: 130rpx;
          height: 130rpx;
        }
      }
    }
    .userInfo {
      text-align: center;
      margin-top: 20rpx;
      font-size: 28rpx;
      color: #fff;
    }
  }
  .bottom {
    padding: 0 20rpx;
    transform: translateY(-26rpx);
    > div {
      background-color: white;
    }
    .history-box {
      display: flex;
      height: 120rpx;
      align-items: center;
      text-align: center;
      color: #aaa;
      font-size: 22rpx;

      .item {
        flex: 1;
      }
    }
    .order {
      margin-top: 20rpx;
      .title {
        font-size: 30rpx;
        height: 90rpx;
        line-height: 90rpx;
        padding-left: 30rpx;
      }
      .order-items {
        display: flex;
        text-align: center;
        align-items: center;
        height: 130rpx;
        .item {
          flex: 1;
          font-size: 24rpx;
        }
        i {
          color: $pinyou;
          font-size: 60rpx;
        }
      }
    }
    .options {
       margin-top: 20rpx;
       padding: 0 20rpx;
      .option {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 84rpx;
        border-bottom: 1rpx solid #ccc;
        font-size: 28rpx;
        &:last-child {
          border-bottom: none;
        }
      }
      i {
        color: #ccc;
      }
    }
  }
}
</style>
