<template>
  <el-row :gutter="20">
	  <div class="background" :style="backgroundImage">
	  </div>
    <el-col :sm="3" class="hidden-xs-only" style="opacity:0;">左侧占位</el-col>
    <el-col :xs="24" :sm="18" style="margin-top: 100px;">
      <el-container>
        <el-timeline class="animate__animated animate__fadeInLeft">
          <el-timeline-item :color="color" v-for="essay in essayList" :key="essay.id" :timestamp="essay.createTime"
            placement="top">
            <el-card
              style="letter-spacing: 1px;border: 1px solid rgba(255,190,23,0.9); background-color: rgba(255,255,255,0.9);box-shadow: 0 0 30px -10px ">
              <h2 v-if="essay.title">{{essay.title}}</h2>
              <div class="typo ql-editor" v-html="essay.content"></div>
            </el-card>
          </el-timeline-item>
        </el-timeline>
      </el-container>
    </el-col>
    <el-col :sm="3" class="hidden-xs-only" style="opacity:0;">右侧占位</el-col>
    <!-- 设置底部距离的 -->
   <el-backtop>
   		  <img src="../../../static/icon/rocket.png" 
   		        style="{
   		          height: 100%;
   		          width: 100%;
   		          text-align: center;
   		          line-height: 40px;
   		          color: #1989fa;
   		        }"
   		      >
   		      </img>
   </el-backtop>   
  </el-row>
</template>

<script>
  import {
    cmsEssayList,
  } from "@/api/cms/blog";
	// 引入背景图
	import backgroundImages from '../backgroundImages.js';
  export default {
    name: 'essay',
    data() {
      return {
        essayList: [],
        // 查询参数
        queryParams: {
          pageNum: 1,
          pageSize: 10,
          title: null,
          type: 2,
          content: null,
          top: null,
          views: null,
          status: null,
		  isReadable: "Y",
        },
        color: "#ffd04b",
		backgroundImages,
      }
    },
	computed: {
		backgroundImage() {
		  // 根据背景图数组的长度随机选择索引
		  const randIndex = Math.floor(Math.random() * this.backgroundImages.length)
		  return {
			// 获取对应的图片资源并将其设置到`background-image`属性上
			backgroundImage: `url(${this.backgroundImages[randIndex]})`
		  }
		},
	},
    created() {
      this.getEssayList()
    },
    methods: {
      async getEssayList() {
        cmsEssayList(this.queryParams).then(response => {
          this.essayList = response.rows;
        });
      },
    }
  }
</script>

<style scoped>
	.background {
	    background-size: cover;
	    margin: 0px;
	    padding: 0px;
	    top: 0;
	    width: 100%;
	    height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		position: absolute;
		z-index: 0;
	  }
  .el-timeline {
    font: 16px/1.5 'Microsoft Yahei', 'PingFang SC', 'Hiragino Sans GB', sans-serif !important;
		margin-top: 70px !important;
    width: 80%;
    margin: 0 auto;
	min-height: 1080px;
  }

  .el-card {
    border-radius: 20px;
    box-shadow: 0 0 15px 5px white;
  }
	/deep/ .el-main {
		 position: relative;
		 z-index: 3;
	}
  @media screen and (max-width: 768px) {
    .el-timeline {
      width: 98%;
      padding: 2px;
    }

    .el-timeline /deep/ .el-timeline-item__wrapper {
      padding-left: 15px !important;
    }
  }
</style>
