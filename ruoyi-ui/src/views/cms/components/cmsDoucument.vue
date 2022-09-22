<template>
  <el-container>
    
  </el-container>
</template>

<script>
  export default {
    name: 'cmsDoucument',
    data() {
      return {}
    },
    mounted() {
      /**
       * iframe-宽高自适应显示
       */
      function changeqtIframe() {
        const qt = document.getElementById('qt')
        const deviceWidth = document.body.clientWidth
        const deviceHeight = document.body.clientHeight
        qt.style.width = Number(deviceWidth) + 'px' // 数字是页面布局宽度差值
        qt.style.height = Number(deviceHeight) + 'px' // 数字是页面布局高度差
      }
      changeqtIframe()
      window.onresize = function() {
        changeqtIframe()
      }
    }
  }
   </script scoped>

  <style scoped rel = "stylesheet/scss"lang = "scss" >
  </style>
