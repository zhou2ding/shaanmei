<template>
  <div class="carriers">

  </div>
</template>

<script setup>
</script>

<style lang="scss" scoped>
@import '@/styles/variables/variables.module';

.carriers {
  position: absolute;
  top: 50px;
  left: 200px;
  height: calc(100vh - 50px);
  width: calc(100vw - 200px);
  background: url('@/assets/images/bg.png') no-repeat center center;
  background-size: cover;
}
</style>