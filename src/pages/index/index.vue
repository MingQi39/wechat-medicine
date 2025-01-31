<template>
  <view class="index-container">
    <view class="header">
      <text class="title">主页</text>
    </view>
    
    <view class="content">
      <text>欢迎使用</text>
    </view>
  </view>
</template>

<script setup lang="ts">
// 主页逻辑代码
</script>

<style lang="scss">
.index-container {
  min-height: 100vh;
  padding: 30rpx;
  
  .header {
    margin-bottom: 30rpx;
    
    .title {
      font-size: 36rpx;
      font-weight: bold;
      color: #333;
    }
  }
  
  .content {
    text-align: center;
    padding: 40rpx 0;
    
    text {
      font-size: 28rpx;
      color: #666;
    }
  }
}
</style>
