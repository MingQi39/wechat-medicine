<template>
  <view class="my-container">
    <view class="user-info">
      <image class="avatar" src="/static/default-avatar.svg" mode="aspectFill"></image>
      <view class="info">
        <text class="nickname">未登录</text>
        <text class="tips">点击登录</text>
      </view>
    </view>

    <view class="menu-list">
      <view class="menu-item" v-for="(item, index) in menuList" :key="index">
        <text class="menu-text">{{ item.text }}</text>
        <text class="arrow">></text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref } from "vue";

const menuList = ref([{ text: "联系客服" }, { text: "设置" }]);
</script>

<style lang="scss">
.my-container {
  min-height: 100vh;
  background-color: #f5f5f5;

  .user-info {
    display: flex;
    align-items: center;
    padding: 40rpx 30rpx;
    background-color: #ffffff;

    .avatar {
      width: 120rpx;
      height: 120rpx;
      border-radius: 50%;
      margin-right: 30rpx;
    }

    .info {
      display: flex;
      flex-direction: column;

      .nickname {
        font-size: 32rpx;
        font-weight: bold;
        margin-bottom: 10rpx;
      }

      .tips {
        font-size: 24rpx;
        color: #999;
      }
    }
  }

  .menu-list {
    margin-top: 20rpx;
    background-color: #ffffff;

    .menu-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 30rpx;
      border-bottom: 1rpx solid #eee;

      .menu-text {
        font-size: 28rpx;
        color: #333;
      }

      .arrow {
        color: #999;
        font-size: 24rpx;
      }

      &:last-child {
        border-bottom: none;
      }
    }
  }
}
</style>
