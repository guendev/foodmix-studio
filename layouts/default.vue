<template>
  <a-layout id="components-layout-demo-custom-trigger">
    <a-layout-sider>
      <div class="site-logo">
        <img src="/favicon/favicon-96x96.png"  alt="" width="40" />
        <p style="color: white">FoodMix</p>
      </div>
      <a-menu theme="dark" mode="inline" :default-selected-keys="['1']">
        <a-menu-item key="1" @click="$router.push({ name: 'recipes' })">
          <a-icon type="appstore" />
          <span>Công Thức</span>
        </a-menu-item>
        <a-menu-item v-if="['mod', 'admin', 'sp_admin'].includes(user.role)" key="2" @click="$router.push({ name: 'categories' })">
          <a-icon type="build" />
          <span>Thể Loại</span>
        </a-menu-item>
        <a-menu-item v-if="['mod', 'admin', 'sp_admin'].includes(user.role)" key="3" @click="$router.push({ name: 'users' })">
          <a-icon type="user" />
          <span>Thành Viên</span>
        </a-menu-item>
        <a-menu-item key="4" @click="logOut()">
          <a-icon type="logout" />
          <span>Đăng Xuất</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout id="base-layout">
      <a-layout-header style="background: #fff; padding: 0">
        <div class="site-header">
          <div class="group-left">
            <a-icon
              class="trigger"
              type="arrow-left"
              @click="$router.back()"
            />
            <portal-target name="title" class="page-title" />
          </div>
          <div class="group-right">
            <portal-target name="action" class="child-group-right" />
          </div>
        </div>
      </a-layout-header>
      <a-layout-content
        :style="{ margin: '24px 16px', padding: '24px', background: '#fff', minHeight: '280px' }"
      >
        <nuxt />
      </a-layout-content>
      <a-layout-footer style="text-align: center">
        FoodMix ©2018 Created by Yuan
      </a-layout-footer>
    </a-layout>
  </a-layout>
</template>
<script>
import { mapGetters } from 'vuex'

export default {
  name: 'DefaultLayout',
  data () {
    return {
      collapsed: false
    }
  },
  computed: {
    ...mapGetters('pref', ['user'])
  },
  methods: {
    logOut () {
      this.$cookies.removeAll()
      location.href = '/'
    }
  }
}
</script>
<style>
#components-layout-demo-custom-trigger {
  display: flex;
  flex-direction: row;
}
#components-layout-demo-custom-trigger .trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color 0.3s;
}

#components-layout-demo-custom-trigger .trigger:hover {
  color: #1890ff;
}

#components-layout-demo-custom-trigger .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
#__layout > * {
  min-height: 100vh;
}
.site-header {
  padding-right: 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.header-title {
  font-size: 20px;
  font-weight: 400;
}
.group-left {
  display: flex;
}

.site-logo p {
  margin-bottom: 0;
  margin-left: 10px;
}

.page-title {
  font-size: 16px;
  font-weight: 400;
}

.row-avatar {
  display: flex;
  align-items: center;
}
.row-avatar img {
  border-radius: 5px;
  margin-right: 10px;
}
.recipe-avatar:hover {
  cursor: pointer !important;
}
.site-logo {
  display: flex;
  align-items: center;
  padding: 10px 20px;
}
</style>
