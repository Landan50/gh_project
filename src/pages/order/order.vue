<template>
  <view class="page">
    <view class="header" :style="{ paddingTop: statusBarHeight + 'px' }">
      <view class="nav">
        <text class="nav-title">我的订单</text>
      </view>
    </view>

    <view class="tabs">
      <view
        class="tab"
        v-for="item in statusTabs"
        :key="item"
        :class="{ active: item === activeTab }"
        @click="switchTab(item)"
      >
        <text class="tab-text">{{ item }}</text>
      </view>
    </view>

    <view class="order-list">
      <view class="order-card" v-for="order in orders" :key="order.id">
        <view class="order-head">
          <text class="order-service">{{ order.service }}</text>
          <text class="order-status" :style="{ color: order.statusColor }">{{ order.status }}</text>
        </view>
        <view class="order-body">
          <view class="order-row">
            <text class="order-label">服务师</text>
            <text class="order-value">{{ order.staff }}</text>
          </view>
          <view class="order-row">
            <text class="order-label">服务时间</text>
            <text class="order-value">{{ order.time }}</text>
          </view>
          <view class="order-row">
            <text class="order-label">订单编号</text>
            <text class="order-value">{{ order.no }}</text>
          </view>
        </view>
        <view class="order-foot">
          <view class="order-price">
            <text class="order-price-label">实付</text>
            <text class="order-price-symbol">¥</text>
            <text class="order-price-value">{{ order.price }}</text>
          </view>
          <view class="order-actions">
            <view class="order-btn ghost" @click="onAction('联系客服')">联系客服</view>
            <view class="order-btn primary" @click="onAction(order.primaryAction)">{{ order.primaryAction }}</view>
          </view>
        </view>
      </view>
    </view>

    <view class="footer-space"></view>

    <app-tab-bar current="order" />
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

const statusTabs = ['全部', '待支付', '进行中', '待评价', '已完成']
const activeTab = ref('全部')

const orders = [
  {
    id: 1,
    service: '日常保洁 3 小时',
    staff: '王阿姨',
    time: '2026-08-25 14:00',
    no: 'JD202608250001',
    price: 99,
    status: '待支付',
    statusColor: '#ff7a45',
    primaryAction: '立即支付'
  },
  {
    id: 2,
    service: '空调深度清洗',
    staff: '李师傅',
    time: '2026-08-24 09:30',
    no: 'JD202608240018',
    price: 129,
    status: '服务中',
    statusColor: '#0f9d8f',
    primaryAction: '查看进度'
  },
  {
    id: 3,
    service: '月嫂咨询 2 小时',
    staff: '张姐',
    time: '2026-08-20 15:00',
    no: 'JD202608200036',
    price: 199,
    status: '待评价',
    statusColor: '#3aa5c9',
    primaryAction: '去评价'
  },
  {
    id: 4,
    service: '全屋收纳整理',
    staff: '周收纳师',
    time: '2026-08-16 10:00',
    no: 'JD202608160052',
    price: 299,
    status: '已完成',
    statusColor: '#9ca3af',
    primaryAction: '再次预约'
  }
]

function switchTab(item) {
  activeTab.value = item
}

function onAction(text) {
  uni.showToast({ title: text + '功能即将上线', icon: 'none' })
}
</script>

<style scoped>
.page {
  min-height: 100vh;
  background-color: #f5f7fa;
}

.header {
  background-color: #ffffff;
  padding-bottom: 20rpx;
}

.nav {
  display: flex;
  align-items: center;
  height: 88rpx;
  padding: 0 24rpx;
}

.nav-title {
  flex: 1;
  text-align: center;
  font-size: 32rpx;
  font-weight: 600;
  color: #1f2937;
}

.tabs {
  display: flex;
  align-items: center;
  padding: 20rpx 24rpx 12rpx;
}

.tab {
  position: relative;
  margin-right: 36rpx;
  padding: 8rpx 0 14rpx;
}

.tab-text {
  font-size: 26rpx;
  color: #6b7280;
}

.tab.active .tab-text {
  font-weight: 600;
  color: #0f9d8f;
}

.tab.active::after {
  content: '';
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translateX(-50%);
  width: 40rpx;
  height: 6rpx;
  border-radius: 3rpx;
  background-color: #0f9d8f;
}

.order-list {
  padding: 12rpx 24rpx 0;
}

.order-card {
  margin-bottom: 24rpx;
  padding: 24rpx;
  border-radius: 24rpx;
  background-color: #ffffff;
}

.order-head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-bottom: 20rpx;
  border-bottom: 1rpx solid #eef0f3;
}

.order-service {
  font-size: 28rpx;
  font-weight: 600;
  color: #1f2937;
}

.order-status {
  font-size: 22rpx;
  font-weight: 600;
}

.order-body {
  padding: 20rpx 0;
}

.order-row {
  display: flex;
  align-items: center;
  margin-bottom: 14rpx;
}

.order-row:last-child {
  margin-bottom: 0;
}

.order-label {
  width: 140rpx;
  font-size: 22rpx;
  color: #9ca3af;
}

.order-value {
  flex: 1;
  font-size: 22rpx;
  color: #4b5563;
}

.order-foot {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 20rpx;
  border-top: 1rpx solid #eef0f3;
}

.order-price {
  display: flex;
  align-items: baseline;
}

.order-price-label {
  margin-right: 8rpx;
  font-size: 22rpx;
  color: #9ca3af;
}

.order-price-symbol {
  font-size: 22rpx;
  font-weight: 600;
  color: #ff7a45;
}

.order-price-value {
  margin-left: 2rpx;
  font-size: 34rpx;
  font-weight: 700;
  color: #ff7a45;
}

.order-actions {
  display: flex;
  align-items: center;
}

.order-btn {
  margin-left: 16rpx;
  padding: 12rpx 26rpx;
  border-radius: 30rpx;
  font-size: 22rpx;
}

.order-btn.ghost {
  color: #4b5563;
  background-color: #f0f3f6;
}

.order-btn.primary {
  color: #ffffff;
  background-color: #0f9d8f;
}

.footer-space {
  height: 180rpx;
}
</style>


