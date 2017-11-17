<template>
  <div class="car_control">
      <transition name="move">
        <div class="reduce_icon" v-show="food.count > 0" @click.stop="reduce_foods"></div>
      </transition>
      <div class="car_count" v-show="food.count > 0">{{food.count}}</div>
      <div class="add_icon" @click.stop="add_foods"></div>
  </div>
</template>
<script>
import Vue from "vue";
export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    add_foods(event) {
      if (!event._constructed) {
        return; 
      }
    //判断移动端：e._constructed 是移动端对象
      if (!this.food.count) {
        Vue.set(this.food, "count", 1);
      } else {
        this.food.count ++;
      }
    },
    reduce_foods() {
      if (this.food.count) {
        this.food.count --;
      }
    }
  }
};
</script>
<style lang="less">
.car_control {
  overflow: hidden;
  &:after {
    content: "";
    display: block;
    clear: both;
  }
  .add_icon {
    width: 30px;
    height: 30px;
    background: url("../../assets/添加.png") no-repeat center;
    background-size: 20px;
    float: left;
  }
  .reduce_icon {
    width: 30px;
    height: 30px;
    background: url("../../assets/减.png") no-repeat center;
    background-size: 20px;
    float: left;

    &.move-enter-active,
    &.move-leave-active {
      transition: all 0.5s;
    }
    &.move-enter,
    &.move-leave-to {
      opacity: 0;
      transform: translateX(20px) rotate(180deg);
    }
  }
  .car_count {
    float: left;
    margin: 0 5px;
    width: 10px;
    height: 30px;
    line-height: 30px;
    font-size: 14px;
    color: #333;
  }
}
</style>


