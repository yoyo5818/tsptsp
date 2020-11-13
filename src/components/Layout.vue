<template>
  <a-layout id="components-layout-demo-side" style="min-height: 100vh">
    <a-layout-sider v-model="collapsed" collapsible>
      <div class="logo" />
      <a-menu theme="dark" :default-selected-keys="['1']" mode="inline">
        <a-menu-item key="1" @click="enterhome">
          <a-icon type="pie-chart" />
          <span>首页</span>
        </a-menu-item>
        <a-menu-item key="2" @click="entermap">
          <a-icon type="desktop" />
          <span>地图展示</span>
        </a-menu-item>
       
        <a-menu-item key="9" @click="analyze">
          <a-icon type="file" />
          <span>tsp分析</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="background: #fff; padding: 0" />
      <a-layout-content style="margin: 0 16px">
        <a-breadcrumb style="margin: 16px 0">
          <a-breadcrumb-item>遗传算法求解TSP</a-breadcrumb-item>
          <a-breadcrumb-item>{{way2}}</a-breadcrumb-item>
        </a-breadcrumb>
        <div :style="{ padding: '24px', background: '#fff', minHeight: '360px' }">
         <router-view/>
         
        </div>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
export default {
  name: 'Layout',
  data() {
    return {
      collapsed: false,
      way2: '首页'
    };
  },
  methods:{
    enterhome: function(){
      this.$router.replace('/home');
      this.way2 = '首页'
    },
    entermap: function(){
      this.$router.replace('/map');
      this.way2 = '地图展示'
    },
	analyze: function(){
	  this.$router.replace('/analyze');
	  this.way2 = '实时分析'
	}
  }
};
</script>

<style>
#components-layout-demo-side .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
.amap-wrapper {
  width: cover;
  height: 500px;
}
</style>
