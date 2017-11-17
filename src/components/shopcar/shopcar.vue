<template>
  <div class="shopcar">
      <div class="shopcar_left">
          <div class="shopcar_icon" :class="{blue_car:total_count > 0}"></div>
          <div class="shopcar_num" v-show="total_count > 0">{{total_count}}</div>
          <div class="shopcar_money">${{total_price}}</div>
          <div class="shopcar_info">另需配送费￥4元</div>
      </div>
      <div class="shopcar_right" :class="{send_ok:this.total_price + 4 > 20}">
          {{total_send}}
      </div>
        <!-- <transition name="moveList">
            <div class="shopcar_list" v-show="show_list">
                <div class="list_top">
                    <div class="list_top_item">购物车</div>
                    <div class="list_top_item" @click="empty_list">清空所有</div>
                </div>
                <div class="list_content" ref="foodList">
                    <ul>
                        <li v-for="food in selectFoods" class="list_item">
                            <div class="list_item_content">{{food.name}}</div>
                            <div class="list_item_content">
                                <div class="price">${{food.price}}</div>
                                <div class="carcontrol_wrapper">
                                    <carcontrol :food="food"></carcontrol>
                                </div>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </transition>
        <transition name="fade">
            <div class="mask" v-show="show_list" @click="hide_list"></div>
        </transition> -->
  </div>
</template>
<script>
import carcontrol from "../carcontrol/carcontrol.vue";
import Bscroll from "better-scroll";
export default {
  data() {
    return {
    };
  },
  props: {
    selectFoods: {
      type: Array
    }
  },
  computed: {
    total_price() {
      var sum = 0;
      for (var i = 0; i < this.selectFoods.length; i++) {
        sum += this.selectFoods[i].count * this.selectFoods[i].price;
      }
      return sum;
    },
    total_count() {
      var num = 0;
      for (var i = 0; i < this.selectFoods.length; i++) {
        num += this.selectFoods[i].count;
      }
      return num;
    },
    total_send() {
      if (this.total_price + 4 <= 20) {
        return "$20元起送";
      } else {
        return "结算";
      }
    }
  },
  methods: {
  },
  components: { carcontrol }
};
</script>
<style lang="less">
.shopcar {
  z-index: 999;
  position: fixed;
  width: 100%;
  height: 55px;
  left: 0;
  bottom: 0;
  background: #0b2042;
  display: flex;

  .shopcar_left {
    z-index: 999;
    flex: 1;
    position: relative;

    .shopcar_icon {
      width: 50px;
      height: 50px;
      position: absolute;
      bottom: 0;
      left: 10px;
      background: #5a5858 url("../../assets/shop_car.png") no-repeat center;
      background-size: 35px;
      border-radius: 50%;
      border: 8px solid #0b2042;

      &.blue_car {
        background: white url("../../assets/shop_car_active.png") no-repeat
          center;
        background-size: 35px;
      }
    }
    .shopcar_num {
      color: white;
      background: red;
      width: 20px;
      height: 20px;
      border-radius: 6px;
      text-align: center;
      line-height: 20px;
      position: absolute;
      top: -8px;
      left: 56px;
    }
    .shopcar_money {
      height: 35px;
      color: white;
      line-height: 35px;
      margin-top: 8px;
      float: left;
      margin-left: 75px;
      font-size: 14px;
      padding-right: 10px;
      border-right: 1px solid #2e4175;
    }
    .shopcar_info {
      height: 55px;
      line-height: 55px;
      color: #9a9a9a;
      font-size: 12px;
      box-sizing: border-box;
      padding: 0 4px;
      text-align: center;
      float: left;
    }
  }
  .shopcar_right {
    z-index: 999;
    flex: 0 0 100px;
    width: 100px;
    background: #000c1f;
    color: #9e9c9c;
    line-height: 55px;
    text-align: center;

    &.send_ok {
      background: green;
      color: white;
    }
  }
  .shopcar_list {
    z-index: 1;
    width: 100%;
    background: white;
    position: fixed;
    bottom: 55px;
    left: 0;
    transform-origin: left bottom;

    &.moveList-enter-active,
    &.moveList-leave-active {
      transition: all 0.5s;
    }
    &.moveList-enter,
    &.moveList-leave-to {
      //   transform: rotateX(45deg);
      transform: translateY(-100px);
      opacity: 0;
    }

    .list_top {
      display: flex;
      justify-content: space-between;
      background: #eee;
      height: 40px;
      line-height: 40px;
      box-sizing: border-box;
      padding: 0 18px;
      font-size: 16px;

      .list_top_item:nth-child(2) {
        color: #0d8ead;
        font-weight: 600;
      }
    }
    .list_content {
      max-height: 200px;
      overflow: hidden;
      ul {
        list-style: none;
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }
      .list_item {
        display: flex;
        justify-content: space-between;
        height: 40px;
        line-height: 40px;
        box-sizing: border-box;
        padding: 0 10px;
        border-bottom: 1px solid #eee;

        .list_item_content {
          .carcontrol_wrapper {
            float: left;
            margin-top: 5px;
            margin-left: 15px;
          }
          .price {
            float: left;
            color: red;
          }
        }
      }
    }
  }
  .mask {
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    top: 0;
    left: 0;
    bottom: 55px;

    &.fade-enter-active,
    &.fade-leave-active {
      transition: all 0.5s;
    }
    &.fade-enter,
    &.fade-leave-to {
      opacity: 0;
    }
  }
}
</style>


