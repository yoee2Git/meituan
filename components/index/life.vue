<template>
  <div class="m-life">
    <el-row>
      <el-col :span="14">
        <carousel />
      </el-col>
      <el-col :span="4">
        <div class="m-life-pic"></div>
      </el-col>
      <el-col :span="6">
        <div class="m-life-login">
          <h4>
            <img src="~/assets/img/titleImg.png" alt />
          </h4>
          <p>Hi 您好 => Yoee</p>
          <p>
            <nuxt-link to="/register">
              <el-button round size="primary">注册</el-button>
            </nuxt-link>
          </p>
          <p>
            <nuxt-link to="/login">
              <el-button round size="medium">立即登录</el-button>
            </nuxt-link>
          </p>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="7">
        <div class="m-life-hotel"></div>
      </el-col>
      <el-col :span="7">
        <div class="m-life-music"></div>
      </el-col>
      <el-col :span="4">
        <div class="m-life-coop"></div>
      </el-col>
      <el-col :span="6">
        <div class="m-life-downloadapp">
          <img src="//s1.meituan.net/bs/fe-web-meituan/60ac9a0/img/download-qr.png" alt />
          <p>美团APP手机版</p>
          <h4>
            <span class="red">1元起</span>
            <em>吃喝玩乐</em>
          </h4>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import carousel from "@/components/index/Carousel.vue";
export default {
  name: "life",
  data() {
    return {};
  },
  components: {
    carousel
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/css/index/life.scss";
</style>