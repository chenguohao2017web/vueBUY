<template>
  <div class="sellerWrapper" ref="sellerWrapper">
      <div class="seller_content">
        <div class="seller_top">
          <div class="seller_info">
            <div class="name">{{seller.name}}</div>
            <div class="starWrapper">
              <star :score="seller.score"></star>
            </div>
            <span class="sellCount">({{seller.sellCount}})</span>
            <span class="mound_sellCount">月售{{seller.ratingCount}}单</span>
            <div class="collect" @click="toogleCollecte">
              <div class="icon" :class="{on:collected}"></div>
              <div v-show="!collected" class="text">收藏</div>
              <div v-show="collected" class="text">已收藏</div>
            </div>
          </div>
          <div class="seller_others">
            <div class="seller_item">
              <div class="title">起送价</div>
              <div class="text"><span class="num">{{seller.minPrice}}</span>元</div>
            </div>
            <div class="seller_item">
               <div class="title">商家配送</div>
              <div class="text"><span class="num">{{seller.deliveryPrice}}</span>元</div>
            </div>
            <div class="seller_item">
               <div class="title">平均配送时间</div>
              <div class="text"><span class="num">{{seller.minPrice}}</span>分钟</div>
            </div>
          </div>
        </div>
        <split></split>
        <div class="seller_public">
          <h1 class="title">公告与活动</h1>
          <p class="text">{{seller.bulletin}}</p>
        </div>
        <split></split>
        <div class="sellerPic">
          <h1 class="title">商家实景</h1>
          <div class="picWrapper" ref="picWrapper">
            <ul class="picUl">
              <li v-for="item in seller.pics" class="pic_item">
                <img :src="item" alt="">
              </li>
            </ul>
          </div>
        </div>
        <split></split>
        <div class="seller_more">
          <h1 class="title">商家信息</h1>
          <ul>
            <li v-for="item in seller.infos" class="sell_more_item">
              {{item}}
            </li>
          </ul>
        </div>
      </div>
  </div>
</template>
<script>
import Bscroll from "better-scroll";
import split from "../split/split";
import star from "../star/star";
export default {
  data(){
    return{
      collected:false
    }
  },
  props: {
    seller: {
      type: Object
    }
  },
  components: { star, split },
  created() {
    this.$nextTick(() => {
      this.picWrapper = new Bscroll(this.$refs.picWrapper, {
        scrollX: true,
        scrollY: false
      });
      this.sellerWrapper = new Bscroll(this.$refs.sellerWrapper, {
        click:true
      });
    });
  },
  methods:{
    toogleCollecte(){
      this.collected = !this.collected;
    }
  }
};
</script>
<style lang="less">
.sellerWrapper {
  position: absolute;
  left: 0;
  top: 163px;
  bottom: 0;
  width: 100%;
  overflow: hidden;

  .seller_content {
    .seller_top {
      padding: 0 18px;

      .seller_info {
        border-bottom: 1px solid #eee;
        position: relative;
        padding: 18px 0;

        .collect {
          position: absolute;
          top: 18px;
          right: 0;
          .icon {
            width: 30px;
            height: 30px;
            background: url("../../assets/心形off.png") no-repeat;
            background-size: 100%;
            margin: 0 auto;
            margin-bottom: 4px;
            &.on{
              background: url("../../assets/心形.png") no-repeat;
            background-size: 100%;
            }
          }
          .text {
            font-size: 10px;
            color: rgb(77, 85, 93);
            line-height: 10px;
            text-align: center;
            width: 36px;
          }
        }
        .name {
          font-size: 16px;
          color: rgb(7, 17, 27);
          line-height: 16px;
          font-weight: 700;
          margin-bottom: 8px;
        }
        .starWrapper {
          display: inline-block;
        }
        .mound_sellCount,
        .sellCount {
          display: inline-block;
          margin-left: 8px;
          font-size: 10px;
          color: rgb(77, 85, 93);
          vertical-align: middle;
          line-height: 10px;
          height: 22px;
        }
      }
      .seller_others {
        padding: 18px 0;
        display: flex;

        .seller_item {
          flex: 1;
          text-align: center;
          border-right: 1px solid #eee;
          &:last-child {
            border-right: none;
          }
          .title {
            font-size: 10px;
            color: rgb(147, 153, 159);
            line-height: 10px;
            margin-bottom: 8px;
          }
          .text {
            .num {
              font-size: 24px;
              font-weight: 200;
              line-height: 24px;
            }
          }
        }
      }
    }
    .seller_public {
      padding: 0 12px;
      .title {
        padding: 18px 0 8px 0;
        font-size: 16px;
        font-weight: 600;
        text-shadow: 1px 1px 4px #eee;
      }
      .text {
        padding: 0 12px;
        font-size: 12px;
        color: rgb(240, 20, 20);
        line-height: 24px;
        padding-bottom: 16px;
      }
    }
    .sellerPic {
      padding: 0 16px;
      .title {
        padding: 18px 0 8px 0;
        font-size: 16px;
        font-weight: 600;
        text-shadow: 1px 1px 4px #eee;
      }
      .picWrapper {
        width: 100%;
        overflow: hidden;

        .picUl {
          width: 538px;

          &:after {
            display: block;
            content: "";
            clear: both;
            padding-bottom: 16px;
          }
          .pic_item {
            width: 130px;
            height: 90px;
            overflow: hidden;
            margin-right: 6px;
            float: left;
            &:last-child {
              margin-right: 0;
            }
          }
        }
      }
    }
    .seller_more {
      padding:0 16px;
      .title {
        font-size: 16px;
        font-weight: 600;
        text-shadow: 1px 1px 4px #eee;
        border-bottom:1px solid #eee;
        padding:12px 0;
      }
      .sell_more_item {
        padding:16px 12px;
        border-bottom:1px solid #eee;
        font-size:12px;
        font-weight:200;
        color:rgb(7,17,27);
        line-height: 16px;
      }
    }
  }
}
</style>

