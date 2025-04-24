<template>
  <div class="main-layout">
    <!-- 左侧导航栏 -->
    <div class="sidebar" :class="{ 'is-collapse': isCollapse }">
      <el-card class="sidebar-card">
        <div class="logo">
          <el-icon><Monitor /></el-icon>
          <span v-show="!isCollapse" class="logo-text">分类系统</span>
        </div>
        <el-menu
          :default-active="activeMenu"
          class="el-menu-vertical"
          :collapse="isCollapse"
          :collapse-transition="false"
        >
          <el-menu-item index="/" @click="router.push('/')">
            <el-icon class="menu-icon"><DataLine /></el-icon>
            <template #title>仪表盘</template>
          </el-menu-item>
        </el-menu>
      </el-card>
    </div>

    <!-- 右侧内容区域 -->
    <div class="main-content">
      <el-card class="content-card">
        <div class="content-header">
          <el-button type="text" @click="toggleCollapse">
            <el-icon :size="20">
              <Fold v-if="!isCollapse"/>
              <Expand v-else/>
            </el-icon>
          </el-button>
        </div>
        <router-view v-slot="{ Component }">
          <transition name="fade" mode="out-in">
            <component :is="Component" />
          </transition>
        </router-view>
      </el-card>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import { Monitor, DataLine, Fold, Expand } from '@element-plus/icons-vue'

const router = useRouter()
const route = useRoute()
const isCollapse = ref(false)

const activeMenu = computed(() => {
  return route.path
})

const toggleCollapse = () => {
  isCollapse.value = !isCollapse.value
}
</script>

<style scoped lang="less">
.main-layout {
  display: flex;
  width: 100vw;
  height: 100vh;
  padding: 16px;
  gap: 16px;
  box-sizing: border-box;
  margin: 0;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  .sidebar {
    transition: all 0.3s ease;
    width: 240px;
    height: 100%;
    flex-shrink: 0;

    &.is-collapse {
      width: 64px;

      .logo {
        padding: 20px 0;
        justify-content: center;

        .el-icon {
          margin: 0;
        }
      }

      :deep(.el-menu) {
        .el-menu-item {
          display: flex;
          justify-content: center;
          padding: 0;
          margin: 8px;
          width: calc(100% - 16px);

          .menu-icon {
            margin: 0;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
          }

          :deep(.el-tooltip__trigger) {
            justify-content: center;
            padding: 0;
          }
        }
      }
    }

    .sidebar-card {
      height: 100%;
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(20px);
      border-radius: 16px;
      border: 1px solid rgba(255, 255, 255, 0.5);
      box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.15);
      transition: all 0.3s ease;
      display: flex;
      flex-direction: column;
      overflow: hidden;

      :deep(.el-card__body) {
        padding: 0;
        flex: 1;
        display: flex;
        flex-direction: column;
        overflow: hidden;
      }

      .logo {
        display: flex;
        align-items: center;
        padding: 20px;
        font-size: 18px;
        font-weight: 600;
        color: var(--el-color-primary);
        border-bottom: 1px solid rgba(255, 255, 255, 0.3);
        margin-bottom: 8px;
        overflow: hidden;
        flex-shrink: 0;
        transition: all 0.3s ease;

        .logo-text {
          margin-left: 12px;
        }

        .el-icon {
          font-size: 24px;
          transition: margin 0.3s ease;
        }
      }

      .el-menu {
        border: none;
        background: transparent;
        flex: 1;

        .el-menu-item {
          height: 50px;
          line-height: 50px;
          margin: 8px;
          border-radius: 8px;
          color: #666;
          padding: 0 20px;
          display: flex;
          align-items: center;

          &:hover, &.is-active {
            color: var(--el-color-primary);
            background: rgba(64, 158, 255, 0.1);
          }

          .menu-icon {
            font-size: 18px;
            margin-right: 12px;
          }
        }
      }
    }
  }

  .main-content {
    flex: 1;
    min-width: 0;
    height: 100%;
    display: flex;
    flex-direction: column;
    overflow: hidden;

    .content-card {
      height: 100%;
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(20px);
      border-radius: 16px;
      border: 1px solid rgba(255, 255, 255, 0.5);
      box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.15);
      transition: all 0.3s ease;
      display: flex;
      flex-direction: column;

      :deep(.el-card__body) {
        padding: 0;
        flex: 1;
        display: flex;
        flex-direction: column;
        overflow: hidden;
      }

      .content-header {
        padding: 16px;
        border-bottom: 1px solid rgba(255, 255, 255, 0.3);
        flex-shrink: 0;

        .el-button {
          padding: 8px;
          color: #666;

          &:hover {
            color: var(--el-color-primary);
          }
        }
      }
    }
  }
}

:deep(.el-menu--collapse) {
  width: 64px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style> 