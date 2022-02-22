<template>
  <div class="main">
    <img src="../assets/下载.png" alt="" />
    <div class="searchContainer">
      <div class="searchBox">
        <input type="text" placeholder="商标名/注册号" v-model="value" />
        <div class="imgSearch">
          <div class="searchIcon" @click="close = !close"></div>
          <div class="searchBtn">搜索</div>
        </div>
      </div>
    </div>
    <div class="searchAdvice" v-if="value">
      <ul>
        <li
          v-for="(item, index) in searchlist"
          :key="item.id"
          @click="active(index)"
          :class="{ active: activeindex === index }"
        >
          <span class="name">{{ item.name }}</span>
          <span class="iconClose" @click.stop="value = ''"></span>
        </li>
      </ul>
    </div>
    <div class="hotSearch">
      <div class="title">
        <span class="hotIcon"></span>
        <span class="hotTitle">热搜:</span>
      </div>
      <div class="hotSearchlist">
        <span class="item">保险</span>
        <span class="item">保险</span>
        <span class="item">保险</span>
        <span class="item">保险</span>
        <span class="item">保险</span>
      </div>
    </div>
    <div class="upload" v-if="close">
      <div class="close" @click="close = !close"></div>
      <el-upload
        class="upload-demo"
        drag
        action="#"
        :on-change="change"
        ref="flie"
      >
        <div class="el-upload__text">拖拽图片到这里</div>
        <div class="el-upload__tip">
          上传说明：图片大小≤MB，尺寸≤1024*1024≥64*64，格式为JPG，PNG
        </div>
        <el-button
          type="primary"
          size="large"
          color="#0000ff"
          style="margin-top: 20px"
          >点击上传</el-button
        >
      </el-upload>
    </div>
    <el-dialog
      v-model="cutting"
      title="图片裁剪"
      width="750px"
      @close="closes"
      destroy-on-close
    >
      <span class="title el-row">
        把不必要的部分裁剪掉，以保证搜索结果的准确性
      </span>
      <VuePictureCropper
        :boxStyle="{
          width: '340px',
          height: 'auto',
          backgroundColor: '#f8f8f8',
          margin: 'auto',
        }"
        :img="pic"
        :options="{
          viewMode: 3,
          dragMode: 'crop',
        }"
      />
      <template #footer>
        <el-button @click="cutting = false">重新上传</el-button>
        <el-button type="primary" @click="cutting = false">确 定</el-button>
      </template>
    </el-dialog>
  </div>
</template>

<script>
import { reactive, ref } from "vue";
import VuePictureCropper, { cropper } from "vue-picture-cropper";
export default {
  components: {
    VuePictureCropper,
  },
  setup() {
    const value = ref("");
    const activeindex = ref(null);
    const close = ref(false);
    const cutting = ref(false);
    const cuttingpic = ref(null); //裁切后的图片
    const pic = ref("");
    const searchlist = reactive([
      {
        name: "沪上阿姨1",
        id: 1,
        show: true,
      },
      {
        name: "沪上阿姨2",
        id: 2,
        show: true,
      },
      {
        name: "沪上阿姨3",
        id: 3,
        show: true,
      },
      {
        name: "沪上阿姨4",
        id: 4,
        show: true,
      },
      {
        name: "沪上阿姨5",
        id: 5,
        show: true,
      },
      {
        name: "沪上阿姨6",
        id: 6,
        show: true,
      },
      {
        name: "沪上阿姨7",
        id: 7,
        show: true,
      },
      {
        name: "沪上阿姨8",
        id: 8,
        show: true,
      },
    ]);
    /**
     * @param {Number} 传入索引
     * @return {Null}
     */
    const active = (index) => {
      activeindex.value = index;
    };
    const change = (file, fileList) => {
      pic.value = window.URL.createObjectURL(file.raw);
      cutting.value = true;
    };
    const closes = () => {
      cropper.getFile().then((result) => {
        cuttingpic.value = window.URL.createObjectURL(result);
        console.log("裁切后的图片", cuttingpic.value);
      });
    };
    return {
      searchlist,
      active,
      value,
      activeindex,
      close,
      cutting,
      change,
      pic,
      closes,
      cropper,
      cuttingpic,
    };
  },
};
</script>

<style lang="less" scoped>
.main {
  // background: #ff6700;
  width: 650px;
  margin: 240px auto 400px;
  display: flex;
  align-items: center;
  flex-direction: column;
  position: relative;
  .upload {
    width: 650px;
    height: 250px;
    background: #fff;
    border-radius: 10px;
    position: absolute;
    top: 200px;
    .close {
      background: url(../assets/关闭.png);
      cursor: pointer;
      position: absolute;
      top: 10px;
      right: 10px;
      background-size: 22px 22px;
      width: 22px;
      height: 22px;
    }
    .upload-demo {
      width: 360px;
      height: 180px;
      margin: 30px auto;
      ::v-deep(.el-upload-dragger) {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
      }
    }
  }
  & img {
    width: 220px;
    height: 76px;
    margin: 0 auto 60px;
  }
  .searchContainer {
    width: 648px;
    margin: 0 auto;
    position: relative;
    .searchBox {
      width: 100%;
      height: 42px;
      border: 1px solid #fff;
      border-radius: 6px;
      & input {
        width: 490px;
        height: 38px;
        justify-content: center;
        margin: 0 0 0 15px;
        padding: 0;
        border: none;
        font-size: 16px;
        color: #fff;
        text-align: left;
        background: none;
        outline: none;
      }
      & input::placeholder {
        color: #ffffff;
      }
      .imgSearch {
        width: 110px;
        position: absolute;
        right: 0;
        top: 3px;
        display: flex;
        align-items: center;
        .searchIcon {
          width: 22px;
          height: 22px;
          background: url(../assets/相机.png);
          background-size: 22px 22px;
          margin-right: 10px;
          cursor: pointer;
        }
        .searchBtn {
          width: 78px;
          height: 34px;
          font-size: 14px;
          color: #396fff;
          display: flex;
          align-items: center;
          justify-content: center;
          margin-right: 3px;
          background: #fff;
          border-radius: 8px;
          cursor: pointer;
        }
      }
    }
  }
  .searchAdvice {
    margin-top: 10px;
    & ul {
      width: 650px;
      max-height: 288px;
      overflow-y: scroll;
      border-radius: 4px;
      background: #fff;
      .active {
        background: #f5f5f5;
        color: #396fff;
      }
      & li {
        width: 100%;
        height: 48px;
        line-height: 48px;
        padding: 0 20px;
        box-sizing: border-box;
        background: #fff;
        font-size: 14px;
        color: #555;
        text-align: left;
        position: relative;
        cursor: pointer;
        .iconClose {
          width: 14px;
          height: 14px;
          background: url(../assets/关闭.png);
          background-size: 14px 14px;
          position: absolute;
          right: 15px;
          top: 17px;
          cursor: pointer;
        }
      }
    }
  }
  .hotSearch {
    width: 540px;
    margin: 25px auto;
    display: flex;
    .title {
      height: 16px;
      display: flex;
      align-items: center;
      margin-top: 3px;

      .hotIcon {
        width: 20px;
        height: 20px;
        background: url(../assets/hot.png);
        background-size: 20px 20px;
        display: inline-block;
        margin-right: 6px;
      }
      .hotTitle {
        font-size: 14px;
        color: #fff;
      }
    }
    .hotSearchlist {
      .item {
        width: 42px;
        height: 14px;
        font-size: 14px;
        margin-left: 20px;
        font-weight: 400;
        color: #ffffff;
        line-height: 14px;
      }
    }
  }
  ::v-deep(.el-dialog__body) {
    text-align: center;
    .title {
      font-size: 16px;
      text-align: center;
      padding-bottom: 20px;
      margin-left: 182px;
    }
  }
  ::v-deep(.el-upload-list) {
    display: none;
  }
}
</style>
