<template>
  <div class="good_list_item" @click="itemClick">
    <img :src="goodsItem.show.img" alt="" @load="imageLoad">
    <div class="description">
      <div class="title">{{ goodsItem.title }}</div>
      <span class="price">{{ goodsItem.price }}</span>
      <span class="collect">{{ goodsItem.cfav }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GoodListItem',
  props: {
    goodsItem: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  methods: {
    //  Vue中通过@load监听图片加载完成事件
    //  原生dom操作，img.onload = function () {....}
    imageLoad () {
      // 通过vue实例发射接收事件
      this.$bus.$emit('itemImageLoad')
    },

    itemClick () {
      this.$router.push('/detail/' + this.goodsItem.iid)
    }
  }
}
</script>

<style lang="less" scoped>
  .good_list_item {
    flex: 1;
    text-align: center;
    width: 36%;
    font-size: 14px;

      img {
        width: 98%;
        border-radius: 5px;
      }

      .title {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        margin: 0 auto;
        width: 80%;
      }

      .price {
        color: deeppink;
      }

      .collect::before {
        display: inline-block;
        content: '';
        width: 16px;
        height: 17px;
        background: url("~assets/img/common/collect.svg") no-repeat 0 2px;
        background-size: 16px;
      }
  }
</style>
