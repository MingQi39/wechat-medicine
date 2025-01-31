<template>
  <view class="my-container">
    <!-- 修改登录区域，使用button组件 -->
    <view class="login-container" v-if="!userInfo.nickName">
      <button class="user-info login-button" open-type="chooseAvatar" @chooseavatar="onChooseAvatar">
        <image class="avatar" :src="avatarUrl || '/static/default-avatar.svg'" mode="aspectFill"></image>
      </button>
      <view class="info">
        <input type="nickname" class="nickname-input" placeholder="请输入昵称" @change="onNicknameChange" />
        <text class="tips">点击头像和输入昵称</text>
      </view>
    </view>

    <!-- 已登录状态显示 -->
    <view v-else class="user-info">
      <image class="avatar" :src="userInfo.avatarUrl" mode="aspectFill"></image>
      <view class="info">
        <text class="nickname">{{ userInfo.nickName }}</text>
        <text class="tips">已登录</text>
      </view>
    </view>

    <view class="menu-list">
      <view class="menu-item" v-for="(item, index) in menuList" :key="index" @tap="handleMenuClick(item)">
        <text class="menu-text">{{ item.text }}</text>
        <text class="arrow">></text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive } from "vue";
import { onShow } from "@dcloudio/uni-app";

interface UserInfo {
  avatarUrl: string;
  nickName: string;
}

const menuList = ref([
  { text: "联系客服", type: "service" },
  { text: "设置", type: "settings" },
]);
const userInfo = reactive<UserInfo>({
  avatarUrl: "",
  nickName: "",
});

const avatarUrl = ref("");

// 修改检查登录状态的函数
onShow(() => {
  const storedUserInfo = uni.getStorageSync("userInfo");
  if (storedUserInfo) {
    Object.assign(userInfo, JSON.parse(storedUserInfo));
  } else {
    // 重置用户信息
    userInfo.avatarUrl = "";
    userInfo.nickName = "";
    avatarUrl.value = "";
  }
});

// 选择头像回调
const onChooseAvatar = (e: any) => {
  avatarUrl.value = e.detail.avatarUrl;
};

// 昵称输入回调
const onNicknameChange = (e: any) => {
  userInfo.nickName = e.detail.value;
  if (avatarUrl.value) {
    userInfo.avatarUrl = avatarUrl.value;
    // 保存用户信息
    uni.setStorageSync("userInfo", JSON.stringify(userInfo));
    uni.showToast({
      title: "设置成功",
      icon: "success",
    });
  }
};

// 添加菜单点击处理函数
const handleMenuClick = (item: { text: string; type: string }) => {
  if (item.type === "settings") {
    uni.navigateTo({
      url: "/pages/my/settings",
    });
  } else if (item.type === "service") {
    // 处理联系客服逻辑
  }
};
</script>

<style lang="scss">
.my-container {
  min-height: 100vh;
  background-color: #f5f5f5;

  .user-info {
    display: flex;
    align-items: center;
    padding: 30rpx;
    background-color: #ffffff;
  }

  .login-container {
    width: 100%;
    height: auto;
    display: flex;
    align-items: center;
    background-color: #ffffff;
  }

  // 登录按钮样式重置
  .login-button {
    margin: 0;
    border: none;
    border-radius: 0;
    padding-right: 0;

    &::after {
      border: none;
    }
  }

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

.nickname-input {
  font-size: 32rpx;
  font-weight: bold;
  margin-bottom: 10rpx;
  width: 200rpx;
}
</style>
