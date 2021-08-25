/*
 * @Author: hjj 
 * @Date: 2021-08-24 11:14:47 
 * @Last Modified by: hjj
 * @Last Modified time: 2021-08-25 17:16:56
 */

<template>
    <el-container style="height: 98vh; border: 1px solid #eee">
        <el-aside width="150px">
            <div class="aside">
                <el-avatar :size="45" icon="el-icon-user-solid"></el-avatar>
                <div>xxx</div>
            </div>
            <el-menu default-active="1" class="el-menu-vertical-demo" background-color="#D3DCE6" text-color="grey" active-text-color="#000">
            <el-menu-item index="1" @click="changeDataQueastion()">
                <i class="el-icon-question"></i>
                <span slot="title">提问</span>
            </el-menu-item>
            <el-menu-item index="2" @click="changeDataAnswer()">
                <i class="el-icon-reading"></i>
                <span slot="title">回答</span>
            </el-menu-item>
            <el-menu-item index="3" @click="changeDataOrder()">
                <i class="el-icon-shopping-bag-2"></i>
                <span slot="title">订单</span>
            </el-menu-item>
            <el-menu-item index="4" @click="changeDataSettings()">
                <i class="el-icon-setting"></i>
                <span slot="title">设置</span>
            </el-menu-item>
        </el-menu>
        </el-aside>
        <el-container>
            <el-header>
                <el-button type="info" icon="el-icon-chat-square" plain>聊天</el-button>
                <el-button type="info" icon="el-icon-bank-card" plain>余额</el-button>
                <el-button type="info" icon="el-icon-thumb" plain>升级</el-button>
            </el-header>
            <el-main>
                <Que v-show="isQuestion"></Que>
                <Ans v-show="isAnswer"></Ans>
                <Ord v-show="isOrder"></Ord>
            </el-main>
        </el-container>
    </el-container>
</template>

<script>
import Que from '@/components/Question.vue'
import Ans from '@/components/Answer.vue'
import Ord from '@/components/Order.vue';

export default {
  name: 'MainPage',
  data () {
    return {
        isQuestion: true,
        isAnswer: false,
        isSettings: false,
        isOrder: false
    }
  },
  methods:{
      changeDataQueastion: function(){
          if(this.isQuestion != true){
              this.isQuestion = true;
              this.isAnswer = false;
              this.isOrder = false;
              this.isSettings = false;
          }
          console.log(this.isQuestion)
      },
      changeDataAnswer: function(){
          console.log(this.isQuestion)
          if(this.isAnswer != true){
              this.isQuestion = false;
              this.isAnswer = true;
              this.isOrder = false;
              this.isSettings = false;
          }
          console.log(this.isQuestion)
      },
      changeDataOrder: function(){
          if(this.isOrder != true){
              this.isQuestion = false;
              this.isAnswer = false;
              this.isOrder = true;
              this.isSettings = false;
          }
      },
      changeDataSettings: function(){
          if(this.isSettings != true){
              this.isQuestion = false;
              this.isAnswer = false;
              this.isOrder = false;
              this.isSettings = true;
          }
      }
  },
  components:{
      Que,
      Ans,
      Ord
  }
}
</script>

<style scoped>
  .el-header{
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
    padding-left: 65vw;
  }
  
  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 100px;
  }
  
  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
  }

  .aside{
    padding-left: 20px;
    padding-right: 20px;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
  }

  .el-menu-vertical-demo {
    width: 150px;
    height: 70vh;
  }

  .el-menu-item{
    height: 15vh;
    padding-left: 4.5vh;
    padding-right: 4.5vh;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
  }
</style>