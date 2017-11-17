<template>
  <div class="ratingSelect">
      <div class="select_cont">
          <span class="select_item all" :class="{on:selectType==2}" @click="selectItem(2)">{{content.all}}<span class="num">{{ratings.length}}</span></span>
          <span class="select_item good" :class="{on:selectType==0}" @click="selectItem(0)">{{content.good}}<span class="num">{{good_num}}</span></span>
          <span class="select_item bad" :class="{on:selectType==1}" @click="selectItem(1)">{{content.bad}}<span class="num">{{bad_num}}</span></span>
      </div>
      <div class="viewHasContent" @click="toggleHasContent">
          <span class="icon" :class="{on:viewHasContent}"></span>
          <span class="text">只看有内容的评价</span>
      </div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
  props: {
    content: {
      type: Object,
      default() {
        return {
          all: "全部",
          good: "推荐",
          bad: "吐槽"
        };
      }
    },
    ratings: {
      type: Array,
      default() {
        return [];
      }
    },
    viewHasContent: {
      type: Boolean,
      default: false
    },
    selectType: {
      type: Number,
      default: 2
    }
  },
  methods: {
    toggleHasContent() {
      this.viewHasContent = !this.viewHasContent;
      this.$emit("viewHasContentEvent", this.viewHasContent);
    },
    selectItem(type) {
      this.selectType = type;
      this.$emit("selectTypeEvent", this.selectType);
    }
  },
  computed: {
    good_num() {
      var arr = [];
      for (var i = 0; i < this.ratings.length; i++) {
        if (this.ratings[i].rateType == 0) {
          arr.push(this.ratings[i]);
        }
      }
      return arr.length;
    },
    bad_num() {
      var arr = [];
      for (var i = 0; i < this.ratings.length; i++) {
        if (this.ratings[i].rateType == 1) {
          arr.push(this.ratings[i]);
        }
      }
      return arr.length;
    }
  }
};
</script>
<style lang="less">
.ratingSelect {
  padding: 0 18px;
  border-bottom:1px solid #eee;

  .select_cont {
    padding: 18px 0;
    font-size: 0;

    .select_item {
      font-size: 12px;
      padding: 8px 12px;
      margin-right: 8px;
      display: inline-block;

      .num {
        font-size: 10px;
        margin-left: 4px;
      }

      &.good,
      &.all {
        color: rgb(77, 85, 93);
        background: rgba(13, 142, 173, 0.2);
        &.on {
          background: #0d8ead;
          color: white;
        }
      }
      &.bad {
        background: rgba(77, 85, 93, 0.2);
        &.on {
          background: rgba(77, 85, 93, 1);
          color: white;
        }
      }
    }
  }
  .viewHasContent {
    padding: 12px 0;
    

    .icon {
      display: inline-block;
      width: 30px;
      height: 30px;
      background: url("../../assets/选中.png") no-repeat center;
      background-size: 100%;
      vertical-align: middle;
      &.on {
        background: url("../../assets/选中on.png") no-repeat center;
        background-size: 100%;
      }
    }
    .text {
      color: rgb(147, 153, 159);
      font-size: 12px;
    }
  }
}
</style>


