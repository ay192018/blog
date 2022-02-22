<template>
  <div class="headbar xs-header">
    <div class="img">
      <a href="javascript:">
        <img src="../assets/下载.png" alt="" />
      </a>
    </div>
    <div class="nav">
      <ul>
        <li class="item" v-for="item in title" :key="item.id">
          {{ item.name }}
        </li>
      </ul>
    </div>
    <div class="login">
      <el-dropdown v-if="token">
        <div class="user">
          <img src="../assets/user.png" alt="" />
          <span>小墨墨</span>
        </div>
        <template #dropdown>
          <el-dropdown-menu>
            <el-dropdown-item>基本资料</el-dropdown-item>
            <el-dropdown-item>浏览记录</el-dropdown-item>
            <el-dropdown-item>打标签记录</el-dropdown-item>
            <el-dropdown-item>订单流水</el-dropdown-item>
            <el-dropdown-item>公证书管理</el-dropdown-item>
            <el-dropdown-item divided @click="token = !token"
              >退出</el-dropdown-item
            >
          </el-dropdown-menu>
        </template>
      </el-dropdown>
      <div class="btn" @click="loginUser" v-else>登录</div>
      <img src="../assets/my.png" class="itemicon" />
      <img src="../assets/classification.png" class="itemicon" />
    </div>
    <el-dialog v-model="login" width="348px" top="30vh">
      <div class="scan">
        <span>微信扫码登录</span>
        <span>刷新</span>
        <span></span>
      </div>
      <img src="../assets/bg.9ca22cf.jpg" class="imgs" alt="" />
      <div class="logins">
        <div class="line"></div>
        <div class="way">登录方式</div>
        <div class="line"></div>
      </div>
      <div class="icons">
        <img src="../assets/ic_wechat_02@2x.png" alt="" />
        <img src="../assets/ic_wechat_02@2x.png" alt="" />
        <img src="../assets/ic_wechat_02@2x.png" alt="" />

        <el-tooltip
          class="box-item"
          effect="dark"
          content="该功能暂未开放"
          placement="bottom-start"
        >
          <img src="../assets/ic_wechat_02@2x.png" alt="" />
        </el-tooltip>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import { reactive, toRefs, ref } from "vue";
export default {
  setup() {
    const login = ref(false);
    const token = ref(false);
    const nav = reactive({
      title: [
        {
          name: "版本系统",
          id: 1,
        },
        {
          name: "版权监测",
          id: 2,
        },
        {
          name: "数字安全",
          id: 3,
        },
        {
          name: "关于我们",
          id: 4,
        },
      ],
    });
    const loginUser = () => {
      login.value = !login.value;
      token.value = !token.value;
    };
    return {
      ...toRefs(nav),
      login,
      token,
      loginUser,
    };
  },
};
</script>

<style lang="less" scoped>
.headbar {
  width: 100%;
  height: 60px;
  background: rgba(0, 0, 0, 0.7);
  .img {
    width: 112px;
    height: 36px;
    position: absolute;
    top: 12px;
    left: 15px;
    & a {
      text-decoration: none;
      color: #232323;
      & img {
        width: 100%;
        height: 100%;
      }
    }
  }
  .nav {
    height: 58px;
    margin-left: 192px;
    cursor: pointer;
    font-size: 14px;
    color: #fff;
    // background: #ff6700;
    & ul {
      margin: 0;
      padding: 0;
      height: 100%;
      .item {
        width: 76px;
        height: 58px;
        margin-right: 40px;
        display: inline-block;
        line-height: 58px;
      }
      .item:hover {
        opacity: 0.65;
      }
    }
  }
  .login {
    height: 56px;
    position: absolute;
    top: 0;
    right: 30px;
    cursor: pointer;
    display: flex;
    align-items: center;
    .user {
      display: flex;
      align-items: center;
      justify-content: space-between;
      & img {
        width: 30px;
        height: 30px;
        margin-right: 10px;
      }
      & span {
        font-size: 16px;

        font-weight: 500;
        color: #ffffff;
      }
    }
    .itemicon {
      display: none;
      width: 28px;
      height: 28px;
      margin-right: 20px;
    }
    .itemicon:nth-child(3) {
      width: 24px;
      height: 24px;
    }
    .btn {
      width: 80px;
      height: 36px;
      line-height: 36px;
      text-align: center;
      font-size: 14px;
      color: #367ffb;
      border-radius: 16px;
      background: #fff;
    }
  }
  ::v-deep(.el-dialog__body) {
    text-align: center;
    height: 424px;
    .scan {
      width: 100%;
      height: 18px;
      font-weight: 500;
      color: #222222;
      line-height: 18px;
      & span {
        margin-left: 10px;
      }
      & span:nth-child(1) {
        font-size: 15px;
        font-weight: 500;
        color: #222222;
        line-height: 18px;
      }
      & span:nth-child(2) {
        height: 12px;
        font-size: 8px;
        font-weight: 400;
        color: #396fff;
        line-height: 12px;
      }
      & span:nth-child(3) {
        display: inline-block;
        width: 12px;
        height: 12px;
        cursor: pointer;
        background: url(../assets/ic_refresh.png);
        background-size: cover;
        vertical-align: middle;
      }
    }
    .imgs {
      margin: 30px 0;
      width: 188px;
      height: 188px;
    }
    .line {
      width: 90px;
      height: 1px;
      opacity: 0.1;
      border: 1px solid #333333;
    }
    .logins {
      display: flex;
      justify-content: space-between;
      align-items: center;
      .way {
        width: 48px;
        height: 12px;
        font-size: 12px;

        font-weight: 400;
        color: #333333;
        line-height: 12px;
      }
    }
    .icons {
      width: 200px;
      margin: 20px auto;
      display: flex;
      justify-content: space-between;
      align-items: center;
      & img {
        width: 30px;
        height: 30px;
        cursor: pointer;
      }
    }
  }
}
</style>
