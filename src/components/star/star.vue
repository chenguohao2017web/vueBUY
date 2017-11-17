<template>
  <div class="star">
      <span v-for="starClass in starClasses" :class="starClass" class="star_item"></span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      length: 5,
      starOn: "on",
      starOff: "off"
    };
  },
  props: {
    score: {
      type: Number,
      default: 2
    }
  },
  computed: {
    starClasses() {
      var arr = [];
      this.score = Math.floor(this.score);
      //on
      for (var i = 0; i < this.score; i++) {
        arr.push(this.starOn);
      }
      for (var i = 0; i < this.length - this.score; i++) {
        arr.push(this.starOff);
      }
      return arr;
    }
  }
};
</script>
<style lang="less">
    .star {
        .star_item {
            display:inline-block;
            width: 20px;
            height: 20px;
            margin-right:2px;
            &.on{
                background:url('../../assets/star_on.png') no-repeat;
                background-size:100%;
            }
            &.off{
                background:url('../../assets/star_off.png') no-repeat;
                background-size:100%;
            }
        }
    }
</style>


