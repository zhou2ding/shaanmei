<template>
  <div id="app">
    <AppSidebar />
    <AppTopBar />
    <div class="main-content">
      <router-view />
    </div>
  </div>
</template>

<script>
import AppSidebar from '@/components/Sidebar/Sidebar.vue';
import AppTopBar from '@/components/TopBar/TopBar.vue'

export default {
  components: {
    AppSidebar,
    AppTopBar,
  },
};
</script>

<style>
#app {
  display: flex;
}

.main-content {
  margin-left: 200px; /* 留出侧边栏的宽度 */
  padding: 20px;
  width: calc(100% - 200px);
}
</style>