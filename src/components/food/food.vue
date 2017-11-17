<template>
  <transition name="go">
    <div class="food" v-show="showFlag" ref="food">
      <div class="food_content">
        <div class="food_img">
          <img :src="food.image" alt="">
          <div class="food_close" @click="food_back"></div>
        </div>
        <div class="content">
          <h1 class="title">{{food.name}}</h1>
          <div class="detail">
            <span class="sell-count">月售{{food.sellCount}}份</span>
            <span class="rating">好评率{{food.rating}}%</span>
          </div>
          <div class="price">
            <span class="new_price">${{food.price}}</span>
            <span class="old_price" v-show="food.oldPrice">{{food.oldPrice}}</span>
          </div>
            <div class="carcontrol_wrapper">
            <carcontrol :food="food"></carcontrol>
          </div>
          <div class="buy" v-show="!food.count || food.count ==0" @click="addFirst">加入购物车</div>
        </div>
        <split v-show="food.info"></split>
        <div class="food_info" v-show="food.info">
          <h1 class="title">商品信息</h1>
          <p class="text">{{food.info}}</p>
        </div>
        <split v-show="food.info"></split>
        <div class="rating">
          <h1 class="title">商品评价</h1>
          <ratingSelect
           :selectType="selectType"
           :viewHasContent="viewHasContent"
           @selectTypeEvent="changeSelectType"
           @viewHasContentEvent="changeViewHasContent"
           :ratings="food.ratings"
           ></ratingSelect>
          <div class="ratingsWrapper" v-show="food.ratings">
              <ul>
                <li v-for="rating in food.ratings" class="rating_item" v-show="selectRating(rating.rateType,rating.text)">
                  <div class="user">
                    <span class="user_name">{{rating.username}}</span>
                    <img :src="rating.avatar" alt="" width="12" height="12">
                  </div>
                  <div class="content_wrapper">
                    <div class="time">
                      {{rating.rateTime | changeTime}}
                    </div>
                    <div class="rating_content">
                      <span class="icon" :class="{on:rating.rateType==1}"></span>
                      <span class="text">{{rating.text}}</span>
                    </div>
                  </div>
                </li>
              </ul>
          </div>
          <div class="noRatings" v-show="!food.ratings">暂无评价</div>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
import ratingSelect from "../ratingselect/ratingselect";
import split from "../split/split";
import Vue from "vue";
import Bscroll from "better-scroll";
import carcontrol from "../carcontrol/carcontrol";
export default {
  props: {
    food: Object
  },
  data() {
    return {
      showFlag: false,
      selectType: 2,
      viewHasContent: false
    };
  },
  methods: {
    show() {
      this.showFlag = true;
      this.$nextTick(() => {
        if (!this.scroll) {
          this.scroll = new Bscroll(this.$refs.food, {
            click: true
          });
        } else {
          this.scroll.refresh();
        }
      });
    },
    food_back() {
      this.showFlag = false;
    },
    addFirst(e) {
      if (!e._constructed) {
        return;
      }
      Vue.set(this.food, "count", 1);
    },
    selectRating(type, text) {
      // 0推荐 1:踩，2全部，
      if (this.viewHasContent && !text) {
        // 如果只看有内容按钮为on 并且 文本内容为空时 这个li不展示
        return false;
      }
      //内容按钮为false  并且类型全部
      if (this.selectType == 2) {
        return true;
      } else {
        return this.selectType == type;
      }
    },
    changeSelectType(type) {
      this.selectType = type;
      this.$nextTick(()=>{
        this.scroll.refresh();
      })
    },
    changeViewHasContent(bool) {
      this.viewHasContent = bool;
      this.$nextTick(()=>{
        this.scroll.refresh();
      })
    }
  },
  components: {
    carcontrol,
    split,
    ratingSelect
  },
  filters:{
    changeTime(time){
      var date = new Date(time);
      var sYear = date.getFullYear() + '';
      var sMonth = date.getMonth() + 1 + '';
      var sDay = date.getDay() + '';
      var sHours = date.getHours() + '';
      var sMinutes = date.getMinutes() + '';
      var sSeconds = date.getSeconds() + '';
      return sYear+'-'+sMonth+'-'+sDay+' '+sHours+':'+sMinutes;
    }
  }
};
</script>
<style lang="less">
.food {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 55px;
  width: 100%;
  background: white;
  z-index: 10px;
  overflow: hidden;

  &.go-enter-active,
  &.go-leave-active {
    transition: all 0.3s;
  }
  &.go-enter,
  &.go-leave-to {
    transform: translateX(100%);
  }
  .food_img {
    position: relative;
    width: 100%;
    height: 0;
    padding-top: 100%;
    img {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }
    .food_close {
      position: absolute;
      top: 10px;
      left: 0;
      width: 25px;
      height: 25px;
      background: url("../../assets/返回.png") no-repeat center;
      background-size: 25px;
      padding: 10px;
    }
  }
  .content {
    padding: 18px;
    box-sizing: border-box;
    position: relative;

    .title {
      margin: 0;
      padding: 0;
      line-height: 14px;
      margin-bottom: 8px;
      font-size: 14px;
      font-weight: 700;
      color: rgb(7, 17, 27);
    }
    .detail {
      margin-bottom: 18px;
      line-height: 10px;
      font-size: 0;
      .sell-count,
      .rating {
        font-size: 10px;
        color: rgb(147, 153, 159);
      }
      .sell-count {
        margin-right: 12px;
      }
    }
    .price {
      font-weight: 700;
      line-height: 24px;

      .new_price {
        margin-right: 8px;
        font-size: 14px;
        color: rgb(240, 20, 20);
      }
      .old_price {
        text-decoration: line-through;
        font-size: 10px;
        color: rgb(147, 153, 159);
      }
    }
    .carcontrol_wrapper {
      position: absolute;
      right: 12px;
      bottom: 12px;
    }
    .buy {
      position: absolute;
      right: 12px;
      bottom: 14px;
      z-index: 9999;
      line-height: 24px;
      padding: 0 12px;
      box-sizing: border-box;
      font-size: 10px;
      border-radius: 12px;
      color: white;
      background: rgb(0, 160, 220);
    }
  }
  .food_info {
    padding: 18px;

    .title {
      line-height: 14px;
      margin-bottom: 6px;
      font-size: 14px;
      color: rgb(7, 17, 27);
    }
    .text {
      margin: 0;
      color: rgb(77, 85, 93);
      line-height: 24px;
      font-size: 12px;
      padding: 0 8px;
    }
  }
  .rating {
    padding-top: 18px;
    .title {
      margin: 0;
      font-size: 14px;
      color: rgb(7, 17, 27);
      margin-left: 18px;
    }
    .ratingsWrapper {
      padding: 0 18px;

      .rating_item {
        position: relative;
        padding: 16px 0;
        border-bottom: 1px solid #eee;

        .user {
          position: absolute;
          right: 0;
          top: 16px;
          .user_name {
            font-size: 10px;
            color: #999;
          }
        }
        .content_wrapper {
          .time {
            color: rgb(147, 153, 159);
            font-size: 12px;
          }
          .rating_content {
            font-size: 0;
            padding-top: 6px;
            .icon {
              display: inline-block;
              width: 20px;
              height: 20px;
              background: url("../../assets/赞.png") no-repeat center;
              background-size: 100%;
              margin-right: 4px;
              &.on {
                background: url("../../assets/踩.png") no-repeat center;
                background-size: 100%;
              }
            }
            .text {
              font-size: 12px;
            }
          }
        }
      }
    }
  }
}
</style>
