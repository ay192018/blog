<template>
  <div class="footer">
    <div class="content">
      <div class="top">
        <span>相关网站：</span>
        <a
          :href="item.url"
          target="_blank"
          v-for="(item, index) in top"
          :key="index"
          >{{ item.name }}</a
        >
      </div>
      <div class="bottom">
        <span
          >Copyright © 2021 郴州市墨贞企业管理合伙企业
          （有限合伙）版权所有</span
        >
        <span
          ><a href="https://beian.miit.gov.cn/" target="_blank"
            >备案号：湘ICP备2021020430号</a
          ></span
        >
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs, } from "vue";
import myHooks from "../hooks/index";
export default {
  setup() {
    const footerlist = reactive({
      top: [
        {
          name: "墨者云",
          url: "https://www.mozheyun.cn",
        },
        {
          name: "易维全",
          url: "http://vquanyi.com/",
        },
        {
          name: "墨者盾",
          url: "https://www.mozhedun.com/",
        },
        {
          name: "至信链",
          url: "https://www.zxinchain.com/",
        },
        {
          name: "蚂蚁链",
          url: "https://antchain.antgroup.com/",
        },
        {
          name: "长安链",
          url: "https://chainmaker.org.cn/",
        },
        {
          name: "中国知产公证平台",
          url: "https://www.ipnotary.com/",
        },
      ],
    });
    const { router, route, store } = myHooks();
    console.log(router, route, store);
    return {
      ...toRefs(footerlist),
      myHooks,
    };
  },
};
</script>

<style lang="less" scoped>
.footer {
  width: 100%;
  min-height: 120px;
  background: #0a1633;
  .content {
    width: 1100px;
    margin: 0 auto;
    padding: 20px 0 24px;
    box-sizing: border-box;
    color: #888;
    .top {
      width: 100%;
      padding-bottom: 18px;
      border-bottom: 1px solid #fff;
      font-size: 12px;
      color: #fff;
      font-weight: 500;
      & a {
        margin-left: 25px;
        color: #fff;
      }
    }
    .bottom {
      margin-top: 24px;
      font-size: 12px;
      color: #fff;
      font-weight: 300;
      & a {
        color: #fff;
      }
    }
  }
}
</style>
>
