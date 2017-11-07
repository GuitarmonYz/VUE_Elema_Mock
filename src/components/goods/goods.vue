<template>
    <div class="goods">
       <div class="menu-wrapper">
        <ul>
            <li v-for="(item, idx) in goods" class="menu-item">
                <span class="text border-1px">
                    <span v-show="item.type > 0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
                </span>
            </li>
        </ul>
       </div>
       <div class="foods-wrapper">
        <ul>
            <li v-for="(item, idx) in goods" class="food-list">
                <h1 class="title">{{item.name}}</h1>
                <ul>
                    <li v-for="food in item.foods" class="food-item">
                        <div class="icon">
                            <img height="57" width="57" :src="food.icon">
                        </div>
                        <div class="content">
                            <h1 class="name">{{food.name}}</h1>
                            <p class="desc">{{food.description}}</p>
                            <div class="extra">
                                <span>Sells count: {{food.sellCount}}</span>
                                <span>Positive Rating Ratio: {{food.rating}}%</span>
                            </div>
                            <div class="price">
                                <span>${{food.price}}</span>
                                <span v-show="food.oldPrice">${{food.oldPrice}}</span>
                            </div>
                        </div>
                    </li>
                </ul>
            </li>
        </ul>
       </div>
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
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = Object.assign({}, this.goods, response.seller);
        }
      });
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin"
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
      .menu-item
        display: table
        height: 54px
        width: 56px
        padding: 0 12px
        line-height: 14px
        .icon
          display: inline-block
          vertical-align: top
          width: 12px
          height: 12px
          margin-right: 2px
          background-size: 12px 12px
          background-repeat: no-repeat
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.guarantee
            bg-image('guarantee_3')
          &.invoice
            bg-image('invoice_3')
          &.special
            bg-image('special_3')
        .text
          display: table-cell
          font-size: 12px
          width: 56px
          vertical-align: middle
          border-1px(rgba(7, 17, 27, 0.7))
    .foods-wrapper
      flex: 1
      .title
        padding-left: 14px
        height: 26px
        line-height: 26px
        border-left: 2px solid #d9dde1
        font-size: 12px
        color: rgb(147, 153, 159)
        background: #f3f5f7
      .food-item
        display: flex
        margin: 18px
        padding-bottom: 18px 
        border-1px(rgba(7, 17, 27, 0.1))
        &: last-child
          border-none()
          margin-bottom: 0
        .icon
          flex: 0 0 57px
          margin-right: 10px
        .content
          margin: 2px 0 8px 0
          height: 14px
          line-height: 14px
          font-size: 14px
          color: rgb(7, 17, 27)  
</style>
