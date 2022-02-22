<template>
  <div class="container">
    <Headbar /><Main /><Footer />
    <div class="contact-items">
      <div class="icon iconQq"></div>
      <span class="line"></span>
      <div class="icon iconHeadset"></div>
      <span class="line"></span>
      <div class="icon iconWechat"></div>
    </div>
    <el-backtop :bottom="80" />
  </div>
</template>
<script>
import Main from "./views/main.vue";
import Headbar from "./views/headbar.vue";
import Footer from "./views/footer.vue";
export default {
  components: { Headbar, Main, Footer },
};
</script>
<style lang="less">
.container {
  width: 100%;
  position: relative;
  .contact-items {
    width: 48px;
    height: 144px;
    border: 2px solid #fff;
    display: flex;
    box-shadow: 0 8px 16px 0 rgb(30 56 127 / 20%);
    flex-direction: column;
    border-radius: 23px;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 50%;
    transform: translateY(-50%);
    right: 20px;
    background: #fff;
    .icon {
      width: 20px;
      height: 20px;
      margin: 14px 0;
      cursor: pointer;
    }
    .iconQq {
      background: url(./assets/qq.png);
      background-size: 20px 20px;
    }
    .iconHeadset {
      background: url(./assets/耳机.png);
      background-size: 20px 20px;
    }
    .iconWechat {
      background: url(./assets/wechat.png);
      background-size: 20px 20px;
    }
    .line {
      width: 16px;
      height: 0;
      border-top: 1px solid #d9d9d9;
      display: inline-block;
    }
  }
}
</style>
