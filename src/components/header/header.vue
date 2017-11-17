<template>
  <div class="header">
      <div class="header_top">
        <div class="header_logo">
          <img :src="childSeller.avatar" alt="">
        </div>
        <div class="header_content">
          <p class="title">{{childSeller.name}}</p>
          <p class="send">{{childSeller.description}}</p>
          <p class="discount">{{childSeller.supports[0].description}}</p>
        </div>
        <div class="more" @click="layout">
          5个<span class="icon"></span>
        </div>
      </div>
      <div class="header_desc" @click="layout">
        {{childSeller.bulletin}}
        <span class="icon"></span>
      </div>
      <transition name="fade">
        <div class="layout" v-show="layout_show">
          <div class="layout_content">
            <h2 class="title">{{childSeller.name}}</h2>
            <p class="text">{{childSeller.bulletin}}</p>
          </div>
          <div class="layout_icon">
            <span class="close_icon" @click="close_layout"></span>
          </div>
        </div>
      </transition>
  </div>
</template>
<script>
export default {
  props: {
    childSeller: {
      type: Object,
      default: function() {
        return {};
      }
    }
  },
  data() {
    return {
      layout_show: false
    };
  },
  methods: {
    layout() {
      this.layout_show = true;
    },
    close_layout(){
      this.layout_show = false;
    }
  }
};
</script>
<style lang="less">
.header {
  width: 100%;
  background: rgba(0, 0, 0, 0.6);

  .header_top {
    width: 100%;
    height: 100px;
    box-sizing: border-box;
    padding: 24px;
    overflow: hidden;
    position: relative;

    .header_logo {
      width: 60px;
      height: 60px;
      float: left;

      img {
        width: 100%;
        height: 100%;
      }
    }
    .header_content {
      height: 60px;
      float: left;
      margin-left: 16px;

      p {
        margin: 0;
        margin-bottom: 4px;
      }

      .title {
        color: white;
      }
      .send,
      .discount {
        color: #ccc;
        font-size: 14px;
      }
    }
    .more {
      position: absolute;
      right: 10px;
      bottom: 10px;
      padding: 6px 12px;
      background: rgba(0, 0, 0, 0.3);
      box-sizing: border-box;
      border-radius: 16px;
      color: white;
      font-size: 14px;
      .icon {
        display: inline-block;
        width: 15px;
        height: 15px;
        background: url("../../assets/下一页.png") no-repeat center center;
        background-size: 15px;
        vertical-align: top;
      }
    }
  }

  .header_desc {
    width: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    padding: 10px 15px;
    box-sizing: border-box;
    font-size: 12px;
    position: relative;
    background: rgba(0, 0, 0, 0.5);
    color: white;

    .icon {
      display: inline-block;
      position: absolute;
      right: 2px;
      bottom: 6px;
      width: 20px;
      height: 20px;
      background: url("../../assets/下一页.png") no-repeat;
      background-size: 20px;
    }
  }
  .layout {
    z-index: 9999999;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.8);

    &.fade-enter-active,
    &.fade-leave-active {
      transition: all 0.5s;
    }
    &.fade-enter,
    &.fade-leave-to {
      opacity: 0;
    }

    .layout_content {
      width: 100%;
      height: 100%;
      box-sizing: border-box;
      padding-bottom: 70px;
      color:white;

     .title {
       text-align: center;
       padding:50px 0;
     }
     .text {
       font-size:12px;
       padding:0 18px;
       line-height: 20px;
     }
    }
    .layout_icon {
      width: 100%;
      margin-top:-70px;
      height: 70px;
      text-align: center;

      .close_icon {
        display: inline-block;
        width:50px;
        height: 50px;
        background:  url('../../assets/关闭.png') no-repeat;
        background-size:50px;
        margin-top:10px;

      }
    }
  }
}
</style>


