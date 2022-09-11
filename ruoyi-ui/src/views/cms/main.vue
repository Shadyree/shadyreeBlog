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
	  padding: 0;
    min-height: 650px;
  }
</style>
