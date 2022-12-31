<template>
  <view class="home-page">
    <view v-for="site in curList" :key="site.name" class="site">
        <nut-button class="btn"
                    type="primary"
                    @click="openSite(site)">
          {{ site.name }}
        </nut-button>
    </view>
  </view>
  <Tabbar @tab-switch="tabSwitch" class="nut-tabbar">
    <TabbarItem tab-title="技术网站" icon="home"></TabbarItem>
    <TabbarItem tab-title="技术团队" icon="find"></TabbarItem>
    <TabbarItem tab-title="大佬们" icon="category"></TabbarItem>
    <TabbarItem tab-title="开源项目" icon="category"></TabbarItem>
    <TabbarItem tab-title="前端周报" icon="category"></TabbarItem>
  </Tabbar>
</template>

<script setup>
import { Tabbar, TabbarItem, Icon } from '@nutui/nutui-taro';
import { sites, teams, developers, projects, weekly } from './sites'
import { ref, computed } from 'vue';

const arr = ref([sites, teams, developers, projects, weekly]);
const curIndex = ref(0);
const curList = computed(() => {
   return arr.value[curIndex.value]
});

const openSite = (site) => {
  // wx.navigateTo({
  //   url: `/pages/link/index?url=${site.link}`
  // })
  wx.setClipboardData({
    data: site.link,
    success: () => {
    }
  })
}

const tabSwitch = (item, index) => {
  curIndex.value = index;
}
</script>

<style lang="scss">
.home-page {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding: 20px;

  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  .site{
    width: 48%;
    margin-bottom: 10px;
  }
  .btn{
    width: 100%;
  }
}
.nut-tabbar{
  position: fixed;
  left: 0;
  bottom: 0;
}
</style>
