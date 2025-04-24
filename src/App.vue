<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <router-view></router-view>
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: linear-gradient(180deg, #B2E4FF 0%, #E6F4FF 100%);
}

#app {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  margin: 0;
  padding: 0;
  background: linear-gradient(180deg, #B2E4FF 0%, #E6F4FF 100%);
}

/* Element Plus 全局样式覆盖 */
:root {
  --el-color-primary: #409EFF;
  --el-border-radius-base: 8px;
}

.el-card {
  --el-card-border-color: rgba(255, 255, 255, 0.5) !important;
  --el-card-border-radius: 16px;
  background: rgba(255, 255, 255, 0.8) !important;
  backdrop-filter: blur(20px) !important;
  border: 1px solid rgba(255, 255, 255, 0.5) !important;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.2) !important;
}

.el-menu {
  --el-menu-hover-bg-color: transparent !important;
  --el-menu-bg-color: transparent !important;
}

.el-menu-item {
  background: transparent !important;
}

.el-menu-item.is-active {
  background: rgba(64, 158, 255, 0.1) !important;
}

.el-menu--collapse {
  .el-menu-item {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 !important;
  }
  
  .el-tooltip__trigger {
    justify-content: center !important;
    padding: 0 !important;
  }
}
</style>
