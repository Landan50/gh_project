<template>
  <view class="page">
    <view class="top" :style="{ paddingTop: statusBarHeight + 'px' }">
      <view class="top-deco deco-a"></view>
      <view class="top-deco deco-b"></view>
      <view class="profile">
        <view class="avatar">
          <text class="avatar-text">家</text>
        </view>
        <view class="profile-info">
          <text class="profile-name">家政用户</text>
          <text class="profile-tip">登录后同步订单与服务进度</text>
        </view>
        <view class="profile-action" @click="onAction('登录')">登录 / 注册</view>
      </view>
    </view>

    <view class="panel order-panel">
      <view class="panel-head">
        <text class="panel-title">我的订单</text>
        <view class="panel-more" @click="goOrder">
          <text class="panel-more-text">全部订单</text>
          <view class="panel-more-arrow"></view>
        </view>
      </view>
      <view class="order-grid">
        <view class="order-item" v-for="item in orderEntries" :key="item.name" @click="goOrder">
          <view class="order-icon" :style="{ backgroundColor: item.bg }">
            <text class="order-glyph" :style="{ color: item.color }">{{ item.glyph }}</text>
          </view>
          <text class="order-name">{{ item.name }}</text>
        </view>
      </view>
    </view>

    <view class="panel menu-panel">
      <view class="menu-item" v-for="item in menus" :key="item.name" @click="onAction(item.name)">
        <view class="menu-icon" :style="{ backgroundColor: item.bg }">
          <text class="menu-glyph" :style="{ color: item.color }">{{ item.glyph }}</text>
        </view>
        <text class="menu-name">{{ item.name }}</text>
        <view class="menu-arrow"></view>
      </view>
    </view>

    <view class="footer-space"></view>
    <app-tab-bar current="mine" />
  </view>
</template>

<script setup>
import { ref } from 'vue'
import AppTabBar from '@/components/app-tab-bar.vue'

const statusBarHeight = ref(20)
try {
  const info = uni.getSystemInfoSync()
  statusBarHeight.value = info.statusBarHeight || 20
} catch (error) {
  statusBarHeight.value = 20
}

const orderEntries = [
  { name: '待支付', glyph: '付', color: '#0f9d8f', bg: 'rgba(15, 157, 143, 0.12)' },
  { name: '服务中', glyph: '服', color: '#3aa5c9', bg: 'rgba(58, 165, 201, 0.12)' },
  { name: '待评价', glyph: '评', color: '#f0a24b', bg: 'rgba(240, 162, 75, 0.14)' },
  { name: '售后', glyph: '后', color: '#ef8d7a', bg: 'rgba(239, 141, 122, 0.14)' }
]

const menus = [
  { name: '地址管理', glyph: '址', color: '#0f9d8f', bg: 'rgba(15, 157, 143, 0.12)' },
  { name: '优惠券', glyph: '券', color: '#f0a24b', bg: 'rgba(240, 162, 75, 0.14)' },
  { name: '收藏服务师', glyph: '藏', color: '#e98b8b', bg: 'rgba(233, 139, 139, 0.14)' },
  { name: '联系客服', glyph: '服', color: '#3aa5c9', bg: 'rgba(58, 165, 201, 0.12)' },
  { name: '关于我们', glyph: '关', color: '#8f7be8', bg: 'rgba(143, 123, 232, 0.14)' },
  { name: '设置', glyph: '设', color: '#7a8699', bg: 'rgba(122, 134, 153, 0.12)' }
]

function goOrder() {
  uni.navigateTo({ url: '/pages/order/order' })
}

function onAction(name) {
  uni.showToast({ title: name + '功能即将上线', icon: 'none' })
}
</script>

<style scoped>
.page {
  min-height: 100vh;
  background-color: #f5f7fa;
}

.top {
  position: relative;
  overflow: hidden;
  padding-bottom: 48rpx;
  background: linear-gradient(135deg, rgba(13, 133, 121, 0.92), rgba(53, 194, 174, 0.78));
}

.top-deco {
  position: absolute;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.12);
}

.deco-a {
  width: 180rpx;
  height: 180rpx;
  right: -40rpx;
  top: 60rpx;
}

.deco-b {
  width: 90rpx;
  height: 90rpx;
  right: 120rpx;
  bottom: -30rpx;
}

.profile {
  display: flex;
  align-items: center;
  padding: 28rpx 32rpx 0;
}

.avatar {
  width: 112rpx;
  height: 112rpx;
  border-radius: 50%;
  border: 4rpx solid rgba(255, 255, 255, 0.72);
  background-color: rgba(255, 255, 255, 0.22);
  display: flex;
  align-items: center;
  justify-content: center;
}

.avatar-text {
  font-size: 44rpx;
  font-weight: 600;
  color: #ffffff;
}

.profile-info {
  flex: 1;
  margin-left: 24rpx;
}

.profile-name {
  display: block;
  font-size: 34rpx;
  font-weight: 600;
  color: #ffffff;
}

.profile-tip {
  display: block;
  margin-top: 8rpx;
  font-size: 22rpx;
  color: rgba(255, 255, 255, 0.85);
}

.profile-action {
  padding: 14rpx 26rpx;
  border-radius: 30rpx;
  background-color: #ffffff;
  font-size: 22rpx;
  font-weight: 600;
  color: #0d8579;
}

.panel {
  margin: 24rpx;
  padding: 28rpx;
  border-radius: 28rpx;
  background-color: #ffffff;
  box-shadow: 0 6rpx 24rpx rgba(15, 23, 42, 0.04);
}

.panel-head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 24rpx;
}

.panel-title {
  font-size: 28rpx;
  font-weight: 600;
  color: #1f2937;
}

.panel-more {
  display: flex;
  align-items: center;
}

.panel-more-text {
  font-size: 22rpx;
  color: #9ca3af;
}

.panel-more-arrow {
  width: 10rpx;
  height: 10rpx;
  margin-left: 6rpx;
  border-top: 2rpx solid #b8c0cc;
  border-right: 2rpx solid #b8c0cc;
  transform: rotate(45deg);
}

.order-grid {
  display: flex;
}

.order-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.order-icon {
  width: 76rpx;
  height: 76rpx;
  border-radius: 22rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.order-glyph {
  font-size: 28rpx;
  font-weight: 600;
}

.order-name {
  margin-top: 12rpx;
  font-size: 22rpx;
  color: #4b5563;
}

.menu-panel {
  padding: 4rpx 24rpx;
}

.menu-item {
  display: flex;
  align-items: center;
  padding: 26rpx 0;
  border-bottom: 1rpx solid #f0f3f6;
}

.menu-item:last-child {
  border-bottom: none;
}

.menu-icon {
  width: 52rpx;
  height: 52rpx;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.menu-glyph {
  font-size: 22rpx;
  font-weight: 600;
}

.menu-name {
  flex: 1;
  margin-left: 20rpx;
  font-size: 26rpx;
  color: #374151;
}

.menu-arrow {
  width: 10rpx;
  height: 10rpx;
  border-top: 2rpx solid #c3cad6;
  border-right: 2rpx solid #c3cad6;
  transform: rotate(45deg);
}

.footer-space {
  height: 180rpx;
}
</style>







