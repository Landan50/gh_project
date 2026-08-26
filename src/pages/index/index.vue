<template>
  <view class="page">
    <view class="header" :style="{ paddingTop: statusBarHeight + 'px' }">
      <view class="nav">
        <view class="location" @click="onLocation">
          <text class="location-city">{{ city }}</text>
          <text class="location-arrow">⌄</text>
        </view>
        <view class="search" @click="onSearch">
          <view class="search-icon"></view>
          <text class="search-text">搜索服务、阿姨或门店</text>
        </view>
        <view class="bell-wrap" @click="onNotice">
          <view class="bell">
            <view class="bell-cap"></view>
          </view>
          <view class="bell-dot"></view>
        </view>
      </view>
    </view>

    <view class="banner">
      <view class="deco deco-1"></view>
      <view class="deco deco-2"></view>
      <view class="deco deco-3"></view>
      <text class="banner-title">全国家政服务</text>
      <text class="banner-sub">300+ 城市覆盖 · 百万家庭信赖</text>
      <view class="banner-tags">
        <text class="banner-tag">持证上岗</text>
        <text class="banner-tag">全程保险</text>
        <text class="banner-tag">售后无忧</text>
      </view>
      <view class="banner-btn" @click="onBook">
        <text class="banner-btn-text">立即预约</text>
      </view>
    </view>

    <view class="section">
      <view class="section-head">
        <text class="section-title">家政服务</text>
        <text class="section-more" @click="onMore">全部分类 ›</text>
      </view>
      <view class="category-grid">
        <view class="category-item" v-for="item in categories" :key="item.name" @click="onService(item.name)">
          <view class="category-icon" :style="{ backgroundColor: item.color }">
            <text class="category-glyph">{{ item.glyph }}</text>
          </view>
          <text class="category-name">{{ item.name }}</text>
        </view>
      </view>
    </view>

    <view class="guarantee">
      <view class="guarantee-item" v-for="item in guarantees" :key="item.text">
        <view class="guarantee-dot" :style="{ backgroundColor: item.color }"></view>
        <text class="guarantee-text">{{ item.text }}</text>
      </view>
    </view>

    <view class="section">
      <view class="section-head">
        <text class="section-title">严选服务师</text>
        <text class="section-more" @click="onMore">查看全部 ›</text>
      </view>
      <scroll-view class="staff-scroll" scroll-x :show-scrollbar="false">
        <view class="staff-card" v-for="staff in staffs" :key="staff.name" @click="onStaff(staff)">
          <view class="staff-avatar" :style="{ backgroundColor: staff.color }">
            <text class="staff-avatar-text">{{ staff.name.slice(0, 1) }}</text>
            <view class="staff-badge">{{ staff.tag }}</view>
          </view>
          <text class="staff-name">{{ staff.name }}</text>
          <view class="staff-meta">
            <text class="staff-score">★ {{ staff.score }}</text>
            <text class="staff-orders">{{ staff.orders }} 单</text>
          </view>
          <text class="staff-city">{{ staff.city }}</text>
        </view>
      </scroll-view>
    </view>

    <view class="section">
      <view class="section-head">
        <text class="section-title">热门服务</text>
        <text class="section-more" @click="onMore">查看更多 ›</text>
      </view>
      <view class="hot-card" v-for="item in hotServices" :key="item.name" @click="onBook">
        <view class="hot-cover" :style="{ backgroundColor: item.color }">
          <text class="hot-glyph">{{ item.glyph }}</text>
        </view>
        <view class="hot-info">
          <view class="hot-name-row">
            <text class="hot-name">{{ item.name }}</text>
            <text class="hot-tag">{{ item.tag }}</text>
          </view>
          <text class="hot-desc">{{ item.desc }}</text>
          <view class="hot-price-row">
            <text class="hot-price-symbol">¥</text>
            <text class="hot-price">{{ item.price }}</text>
            <text class="hot-unit">{{ item.unit }}</text>
          </view>
        </view>
      </view>
    </view>

    <view class="footer-space"></view>

    <view class="book-bar">
      <view class="book-info">
        <text class="book-title">全国统一服务热线</text>
        <text class="book-phone">400-888-0000</text>
      </view>
      <view class="book-btn" @click="onBook">
        <text class="book-btn-text">立即预约</text>
      </view>
    </view>

    <app-tab-bar current="index" />
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

const city = ref('上海')

const categories = [
  { name: '日常保洁', glyph: '洁', color: '#0e9c90' },
  { name: '深度清洁', glyph: '深', color: '#11a99c' },
  { name: '家电清洗', glyph: '电', color: '#14b5a7' },
  { name: '保姆月嫂', glyph: '嫂', color: '#17bfb0' },
  { name: '搬家搬运', glyph: '搬', color: '#1bc7b8' },
  { name: '维修安装', glyph: '修', color: '#23cbbc' },
  { name: '上门做饭', glyph: '饭', color: '#31cfc0' },
  { name: '衣物洗护', glyph: '衣', color: '#3fd3c4' }
]

const guarantees = [
  { text: '严格培训', color: '#0f9d8f' },
  { text: '持证上岗', color: '#0f9d8f' },
  { text: '全程保险', color: '#0f9d8f' },
  { text: '售后无忧', color: '#0f9d8f' }
]

const staffs = [
  { name: '王阿姨', tag: '金牌保洁', score: 4.9, orders: 1280, city: '上海', color: '#0f9d8f' },
  { name: '李师傅', tag: '家电清洗', score: 4.8, orders: 936, city: '成都', color: '#3aa5c9' },
  { name: '张姐', tag: '母婴护理', score: 5.0, orders: 1562, city: '广州', color: '#f0a24b' }
]

const hotServices = [
  { name: '日常保洁 3 小时', desc: '专业阿姨上门 · 自备工具', price: 99, unit: '起', tag: '热销', glyph: '洁', color: '#0f9d8f' },
  { name: '空调深度清洗', desc: '高温蒸汽除菌 · 拆洗滤网', price: 129, unit: '台', tag: '特惠', glyph: '洗', color: '#3aa5c9' },
  { name: '月嫂 / 育儿嫂', desc: '持证上岗 · 视频面试', price: 8000, unit: '月起', tag: '严选', glyph: '月', color: '#f0a24b' },
  { name: '全屋收纳整理', desc: '空间规划 · 物归其位', price: 299, unit: '起', tag: '新品', glyph: '收', color: '#17b3a1' }
]

function showTip(title) {
  uni.showToast({ title, icon: 'none' })
}

function onSearch() {
  showTip('搜索功能即将上线')
}

function onLocation() {
  showTip('城市切换即将上线')
}

function onNotice() {
  showTip('暂无新消息')
}

function onMore() {
  showTip('更多功能即将上线')
}

function onService(name) {
  showTip(name + '服务即将上线')
}

function onStaff(staff) {
  showTip('查看' + staff.name)
}

function onBook() {
  showTip('预约功能即将上线')
}

</script>

<style scoped>
.page {
  min-height: 100vh;
  background-color: #f5f7fa;
}

.header {
  background-color: #ffffff;
  padding: 0 24rpx 20rpx;
}

.nav {
  display: flex;
  align-items: center;
  height: 88rpx;
}

.location {
  display: flex;
  align-items: center;
  margin-right: 16rpx;
}

.location-city {
  max-width: 140rpx;
  font-size: 28rpx;
  font-weight: 600;
  color: #1f2937;
}

.location-arrow {
  margin-left: 4rpx;
  font-size: 26rpx;
  color: #9ca3af;
}

.search {
  flex: 1;
  height: 64rpx;
  background-color: #f0f3f6;
  border-radius: 32rpx;
  display: flex;
  align-items: center;
  padding: 0 24rpx;
}

.search-icon {
  width: 22rpx;
  height: 22rpx;
  border: 3rpx solid #9ca3af;
  border-radius: 50%;
  position: relative;
  margin-right: 14rpx;
}

.search-icon::after {
  content: '';
  position: absolute;
  width: 3rpx;
  height: 12rpx;
  background-color: #9ca3af;
  right: -7rpx;
  bottom: -7rpx;
  transform: rotate(-45deg);
}

.search-text {
  font-size: 24rpx;
  color: #9ca3af;
}

.bell-wrap {
  margin-left: 20rpx;
  position: relative;
  width: 56rpx;
  height: 56rpx;
  border-radius: 28rpx;
  background-color: #f0f3f6;
  display: flex;
  align-items: center;
  justify-content: center;
}

.bell {
  width: 26rpx;
  height: 26rpx;
  border: 3rpx solid #4b5563;
  border-radius: 14rpx 14rpx 12rpx 12rpx;
  position: relative;
}

.bell::after {
  content: '';
  position: absolute;
  left: -5rpx;
  bottom: -7rpx;
  width: 30rpx;
  height: 3rpx;
  background-color: #4b5563;
  border-radius: 2rpx;
}

.bell-cap {
  position: absolute;
  left: 50%;
  top: -8rpx;
  width: 6rpx;
  height: 9rpx;
  background-color: #4b5563;
  border-radius: 3rpx;
  transform: translateX(-50%);
}

.bell-dot {
  position: absolute;
  top: 10rpx;
  right: 10rpx;
  width: 12rpx;
  height: 12rpx;
  border-radius: 50%;
  background-color: #ff7a45;
  border: 2rpx solid #ffffff;
}

.banner {
  position: relative;
  overflow: hidden;
  margin: 24rpx;
  border-radius: 28rpx;
  padding: 40rpx 32rpx 36rpx;
  background: linear-gradient(135deg, #0b877c, #2fc0a6);
}

.deco {
  position: absolute;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.14);
}

.deco-1 {
  width: 240rpx;
  height: 240rpx;
  right: -60rpx;
  top: -80rpx;
}

.deco-2 {
  width: 140rpx;
  height: 140rpx;
  right: 90rpx;
  bottom: -60rpx;
}

.deco-3 {
  width: 60rpx;
  height: 60rpx;
  right: 44rpx;
  top: 52rpx;
}

.banner-title {
  font-size: 42rpx;
  font-weight: 700;
  color: #ffffff;
}

.banner-sub {
  margin-top: 12rpx;
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.92);
}

.banner-tags {
  margin-top: 26rpx;
  display: flex;
}

.banner-tag {
  margin-right: 14rpx;
  padding: 8rpx 16rpx;
  border-radius: 20rpx;
  font-size: 20rpx;
  color: #0b877c;
  background-color: rgba(255, 255, 255, 0.94);
}

.banner-btn {
  position: absolute;
  right: 32rpx;
  bottom: 36rpx;
  padding: 14rpx 30rpx;
  border-radius: 32rpx;
  background-color: #ffffff;
}

.banner-btn-text {
  font-size: 24rpx;
  font-weight: 600;
  color: #0b877c;
}

.section {
  margin: 24rpx;
}

.section-head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20rpx;
}

.section-title {
  font-size: 32rpx;
  font-weight: 600;
  color: #1f2937;
}

.section-more {
  font-size: 22rpx;
  color: #9ca3af;
}

.category-grid {
  display: flex;
  flex-wrap: wrap;
  padding: 24rpx 8rpx 8rpx;
  border-radius: 24rpx;
  background-color: #ffffff;
}

.category-item {
  width: 25%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 16rpx 0 20rpx;
}

.category-icon {
  width: 88rpx;
  height: 88rpx;
  border-radius: 24rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.category-glyph {
  font-size: 36rpx;
  font-weight: 600;
  color: #ffffff;
}

.category-name {
  margin-top: 12rpx;
  font-size: 22rpx;
  color: #4b5563;
}

.guarantee {
  margin: 0 24rpx;
  padding: 24rpx 20rpx;
  border-radius: 20rpx;
  background-color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.guarantee-item {
  display: flex;
  align-items: center;
}

.guarantee-dot {
  width: 12rpx;
  height: 12rpx;
  border-radius: 50%;
  margin-right: 8rpx;
}

.guarantee-text {
  font-size: 22rpx;
  color: #4b5563;
}

.staff-scroll {
  white-space: nowrap;
}

.staff-card {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  width: 220rpx;
  margin-right: 20rpx;
  padding: 28rpx 16rpx 24rpx;
  border-radius: 24rpx;
  background-color: #ffffff;
  vertical-align: top;
}

.staff-avatar {
  position: relative;
  width: 120rpx;
  height: 120rpx;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.staff-avatar-text {
  font-size: 44rpx;
  font-weight: 600;
  color: #ffffff;
}

.staff-badge {
  position: absolute;
  left: 50%;
  bottom: -10rpx;
  transform: translateX(-50%);
  padding: 2rpx 12rpx;
  border-radius: 16rpx;
  border: 1rpx solid #0f9d8f;
  background-color: #ffffff;
  font-size: 18rpx;
  color: #0f9d8f;
  white-space: nowrap;
}

.staff-name {
  margin-top: 26rpx;
  font-size: 26rpx;
  font-weight: 600;
  color: #1f2937;
}

.staff-meta {
  margin-top: 10rpx;
  display: flex;
  align-items: center;
}

.staff-score {
  font-size: 20rpx;
  color: #f0a24b;
}

.staff-orders {
  margin-left: 12rpx;
  font-size: 20rpx;
  color: #9ca3af;
}

.staff-city {
  margin-top: 6rpx;
  font-size: 20rpx;
  color: #9ca3af;
}

.hot-card {
  display: flex;
  margin-bottom: 20rpx;
  padding: 20rpx;
  border-radius: 24rpx;
  background-color: #ffffff;
}

.hot-card:last-child {
  margin-bottom: 0;
}

.hot-cover {
  width: 160rpx;
  height: 160rpx;
  border-radius: 20rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hot-glyph {
  font-size: 52rpx;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
}

.hot-info {
  flex: 1;
  margin-left: 24rpx;
  padding: 6rpx 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.hot-name-row {
  display: flex;
  align-items: center;
}

.hot-name {
  font-size: 28rpx;
  font-weight: 600;
  color: #1f2937;
}

.hot-tag {
  margin-left: 12rpx;
  padding: 4rpx 12rpx;
  border-radius: 12rpx;
  background-color: rgba(255, 122, 69, 0.12);
  font-size: 18rpx;
  color: #ff7a45;
}

.hot-desc {
  font-size: 22rpx;
  color: #9ca3af;
}

.hot-price-row {
  display: flex;
  align-items: baseline;
}

.hot-price-symbol {
  font-size: 22rpx;
  font-weight: 600;
  color: #ff7a45;
}

.hot-price {
  margin-left: 2rpx;
  font-size: 36rpx;
  font-weight: 700;
  color: #ff7a45;
}

.hot-unit {
  margin-left: 4rpx;
  font-size: 20rpx;
  color: #ff7a45;
}

.footer-space {
  height: 280rpx;
}

.book-bar {
  position: fixed;
  left: 24rpx;
  right: 24rpx;
  bottom: calc(120rpx + env(safe-area-inset-bottom));
  z-index: 20;
  padding: 16rpx 20rpx;
  border-radius: 24rpx;
  background-color: #ffffff;
  box-shadow: 0 8rpx 32rpx rgba(15, 23, 42, 0.08);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.book-title {
  display: block;
  font-size: 20rpx;
  color: #9ca3af;
}

.book-phone {
  display: block;
  margin-top: 4rpx;
  font-size: 30rpx;
  font-weight: 700;
  color: #1f2937;
}

.book-btn {
  padding: 18rpx 36rpx;
  border-radius: 40rpx;
  background: linear-gradient(135deg, #0b877c, #17b39a);
}

.book-btn-text {
  font-size: 26rpx;
  font-weight: 600;
  color: #ffffff;
}

.tab-bar {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 30;
  padding: 12rpx 0 calc(12rpx + env(safe-area-inset-bottom));
  border-top: 1rpx solid #eef0f3;
  background-color: #ffffff;
  display: flex;
}

.tab-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.tab-icon {
  width: 56rpx;
  height: 56rpx;
  border-radius: 18rpx;
  background-color: #f0f3f6;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tab-icon.active {
  background-color: rgba(15, 157, 143, 0.12);
}

.tab-glyph {
  font-size: 26rpx;
  color: #6b7280;
}

.tab-icon.active .tab-glyph {
  font-weight: 700;
  color: #0f9d8f;
}

.tab-name {
  margin-top: 6rpx;
  font-size: 20rpx;
  color: #6b7280;
}

.tab-name.active {
  font-weight: 600;
  color: #0f9d8f;
}
</style>


