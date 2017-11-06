<template>
    <div class="goods">
       <div class="menu-wrapper"></div>
       <div class="foods-wrapper"></div>
    </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0;
  export default {
    probs: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        goods: []
      };
    },
    created () {
      this.$http.get('api/goods').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = Object.assign({}, this.goods, response.goods);
        }
      });
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .goods
    position: absolute
    display: flex
    top: 174px
    width: 100%
    bottom: 46px
    overflow: hidden
    .menu-wrapper
      flex: 0 0 80px
      width: 80px
      background: #f3f5f7 
    .foods-wrapper
      flex: 1
</style>
