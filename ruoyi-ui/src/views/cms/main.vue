<template>
    <el-main>
      <router-view :key="key" />
    </el-main>
</template>

<script>
  export default {
    name: 'cmsMain',
    computed: {
      key() {
        return this.$route.path
      }
    }
  }
</script>

<style scoped>
  .el-main {
	  /* 所有页面的样式，引用组件了的都从这里走 */
	padding: 0;
	min-height: 120vh;
	overflow: hidden;
  }
</style>
