<script setup lang="ts">
import { h, ref } from 'vue'
import { HomeOutlined, GithubOutlined, LinkOutlined } from '@ant-design/icons-vue'
import { MenuProps } from 'ant-design-vue'
import { useRouter } from 'vue-router'
import { useLoginUserStore } from '@/stores/useLoginUserStore.ts'

const loginUserStore = useLoginUserStore()
const items = ref<MenuProps['items']>([
  {
    key: '/',
    icon: () => h(HomeOutlined),
    label: '主页',
    title: '主页',
  },
  {
    key: '/about',
    icon: () => h(LinkOutlined),
    label: '关于',
    title: '关于',
  },
  {
    key: '/other',
    icon: () => h(GithubOutlined),
    label: h('a', { href: 'https://github.com/vuejs/core', target: '_blank' }, 'Github'),
    title: 'Github',
  },
])
const router = useRouter()

const current = ref<string[]>(['/'])
// 每次进入新页面都会调用这个函数
router.afterEach((to) => {
  current.value = [to.path]
})

// 路由跳转事件
const doMenuClick = ({ key }) => {
  router.push({
    path: key,
  })
}
</script>

<template id="globalHeader">
  <a-row :wrap="false">
    <a-col flex="200px">
      <router-link to="/">
        <div class="title-bar">
          <img class="logo" src="../assets/logo.png" alt="logo" />
          <div class="title">智能云图库</div>
        </div>
      </router-link>
    </a-col>
    <a-col flex="auto">
      <a-menu
        v-model:selectedKeys="current"
        mode="horizontal"
        :items="items"
        @click="doMenuClick"
      />
    </a-col>
    <a-col flex="100px">
      <div class="user-login-status">
        <div v-if="loginUserStore.loginUser.id">
          {{ loginUserStore.loginUser.userName ?? '无名' }}
        </div>
        <div v-else>
          <a-button type="primary">登录</a-button>
        </div>
      </div>
    </a-col>
  </a-row>
</template>

<style scoped>
.title-bar {
  display: flex;
  align-items: center;
}
.title {
  color: black;
  font-size: 18px;
  margin-left: 16px;
}
.logo {
  height: 48px;
}
</style>
