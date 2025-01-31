<template>
  <view class="settings-container">
    <view class="menu-list">
      <!-- 可以在这里添加其他设置项 -->
      <button class="logout-btn" @tap="handleLogout">退出登录</button>
    </view>
  </view>
</template>

<script setup lang="ts">
const handleLogout = () => {
  uni.showModal({
    title: "提示",
    content: "确定要退出登录吗？",
    success: (res) => {
      if (res.confirm) {
        // 清除用户信息
        uni.removeStorageSync("userInfo");
        uni.showToast({
          title: "已退出登录",
          icon: "success",
        });
        // 返回上一页
        setTimeout(() => {
          uni.navigateBack();
        }, 1500);
      }
    },
  });
};
</script>

<style lang="scss">
.settings-container {
  min-height: 100vh;
  background-color: #f5f5f5;

  .menu-list {
    margin-top: 20rpx;
    padding: 0 30rpx;
  }

  .logout-btn {
    margin-top: 30rpx;
    background-color: $uni-color-primary;
    color: #fff;

    &:active {
      opacity: 0.8;
    }
  }
}
</style>
