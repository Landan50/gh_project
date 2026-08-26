<template>
  <view class="tab-bar">
    <view class="tab-item" v-for="tab in tabs" :key="tab.key" @click="onTab(tab)">
      <view class="tab-icon" :class="{ active: tab.key === current }">
        <text class="tab-glyph">{{ tab.glyph }}</text>
      </view>
      <text class="tab-name" :class="{ active: tab.key === current }">{{ tab.name }}</text>
    </view>
  </view>
</template>

<script setup>
const props = defineProps({
  current: {
    type: String,
    default: 'index'
  }
})

const tabs = [
  { key: 'index', name: '首页', glyph: '首' },
  { key: 'order', name: '订单', glyph: '单' },
  { key: 'message', name: '消息', glyph: '信' },
  { key: 'mine', name: '我的', glyph: '我' }
]

function onTab(tab) {
  if (tab.key === props.current) return
  if (tab.key === 'index') {
    uni.reLaunch({ url: '/pages/index/index' })
  } else if (tab.key === 'order') {
    uni.navigateTo({ url: '/pages/order/order' })
  } else if (tab.key === 'mine') {
    uni.navigateTo({ url: '/pages/mine/mine' })
  } else {
    uni.showToast({ title: tab.name + '模块即将上线', icon: 'none' })
  }
}
</script>

<style scoped>
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

