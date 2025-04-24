<template>
  <div class="dashboard">
    <div class="dashboard-header">
      <h2>仪表盘</h2>
      <el-breadcrumb separator="/">
        <el-breadcrumb-item>首页</el-breadcrumb-item>
        <el-breadcrumb-item>仪表盘</el-breadcrumb-item>
      </el-breadcrumb>
    </div>

    <div class="dashboard-content">
      <!-- 统计卡片 -->
      <div class="stat-cards">
        <el-row :gutter="16">
          <el-col :span="6" v-for="(stat, index) in stats" :key="index">
            <el-card class="stat-card" shadow="hover">
              <div class="stat-icon">
                <el-icon :size="24">
                  <component :is="stat.icon" />
                </el-icon>
              </div>
              <div class="stat-info">
                <div class="stat-value">{{ stat.value }}</div>
                <div class="stat-label">{{ stat.label }}</div>
              </div>
            </el-card>
          </el-col>
        </el-row>
      </div>

      <!-- 欢迎卡片 -->
      <el-card class="welcome-card">
        <template #header>
          <div class="welcome-header">
            <span>欢迎使用</span>
            <el-tag size="small" effect="plain" type="primary">Beta</el-tag>
          </div>
        </template>
        <div class="welcome-content">
          <el-empty description="开始使用分类系统">
            <el-button type="primary">开始使用</el-button>
          </el-empty>
        </div>
      </el-card>
    </div>
  </div>
</template>

<script setup lang="ts">
import {
  DataLine,
  User,
  Document,
  Collection
} from '@element-plus/icons-vue'

const stats = [
  {
    label: '总访问量',
    value: '1,234',
    icon: DataLine
  },
  {
    label: '用户数',
    value: '56',
    icon: User
  },
  {
    label: '文档数',
    value: '89',
    icon: Document
  },
  {
    label: '分类数',
    value: '12',
    icon: Collection
  }
]
</script>

<style scoped lang="less">
.dashboard {
  height: 100%;
  display: flex;
  flex-direction: column;
  overflow: hidden;

  .dashboard-header {
    padding: 24px 24px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-shrink: 0;

    h2 {
      margin: 0;
      font-size: 20px;
      font-weight: 600;
      color: #333;
    }
  }

  .dashboard-content {
    padding: 24px;
    flex: 1;
    overflow: auto;
    min-height: 0;

    .stat-cards {
      margin-bottom: 24px;

      :deep(.el-row) {
        margin-bottom: -16px;
        margin-right: -8px;
        margin-left: -8px;
      }

      :deep(.el-col) {
        padding-bottom: 16px;
        padding-right: 8px;
        padding-left: 8px;
      }

      .stat-card {
        background: rgba(255, 255, 255, 0.85);
        border: 1px solid rgba(255, 255, 255, 0.5);
        backdrop-filter: blur(20px);
        transition: all 0.3s ease;
        height: 100%;
        position: relative;
        overflow: hidden;

        &::before {
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          height: 4px;
          background: linear-gradient(90deg, #409EFF, #79bbff);
          opacity: 0.8;
          transition: all 0.3s ease;
        }

        :deep(.el-card__body) {
          padding: 20px;
          display: flex;
          align-items: center;
          gap: 16px;
          height: 100%;
        }

        .stat-icon {
          width: 48px;
          height: 48px;
          border-radius: 12px;
          background: var(--el-color-primary-light-9);
          display: flex;
          align-items: center;
          justify-content: center;
          color: var(--el-color-primary);
          transition: all 0.3s ease;
        }

        .stat-info {
          flex: 1;

          .stat-value {
            font-size: 24px;
            font-weight: 600;
            color: #333;
            line-height: 1.2;
          }

          .stat-label {
            font-size: 14px;
            color: #666;
            margin-top: 4px;
          }
        }

        &:hover {
          transform: translateY(-2px);
          box-shadow: 0 8px 24px rgba(31, 38, 135, 0.15);

          &::before {
            height: 6px;
            opacity: 1;
          }

          .stat-icon {
            transform: scale(1.1);
          }
        }
      }
    }

    .welcome-card {
      background: rgba(255, 255, 255, 0.85);
      border: 1px solid rgba(255, 255, 255, 0.5);
      backdrop-filter: blur(20px);
      flex: 1;
      display: flex;
      flex-direction: column;
      min-height: 400px;
      position: relative;
      overflow: hidden;

      &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 4px;
        background: linear-gradient(90deg, #409EFF, #79bbff);
        opacity: 0.8;
        transition: all 0.3s ease;
      }

      &:hover::before {
        height: 6px;
        opacity: 1;
      }

      :deep(.el-card__body) {
        flex: 1;
        display: flex;
        flex-direction: column;
      }

      .welcome-header {
        display: flex;
        align-items: center;
        gap: 12px;
        font-size: 16px;
        font-weight: 500;
      }

      .welcome-content {
        padding: 40px 0;
        flex: 1;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }
  }
}
</style> 