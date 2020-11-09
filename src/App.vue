<template>
  <div>
    <button>点我有惊喜</button>
    <router-link to="">测试</router-link>
    <router-view></router-view>
     <el-carousel height="150px">
      <el-carousel-item v-for="item in 4" :key="item">
        <h3 class="small">{{ item }}</h3>
      </el-carousel-item>
    </el-carousel>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="less">
  div {

    button {
      background-color: cyan;
    }
  }
</style>