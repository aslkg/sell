<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menu-wrapper">
      <ul>
        <li v-for="item in goods" :key="item.key" class="menu-item">
          <span class="text tab">
            <span v-show="item.type > 0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foods-wrapper">
      <ul>
        <li v-for="item in goods" :key="item.key" class="good-list">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" :key="food.key" class="food-item tab">
              <div class="icon">
                <img width="57" height="57" :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// import BScroll from 'better-scroll'

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: []
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    this.$axios.get('/api/goods').then((res) => {
      if (res.status === 200) {
        this.goods = res.data.data
        this._initScroll()
      }
    })
  }
  // methods: {
  //   _initScroll () {
  //     this.menuScroll = new BScroll(this.$refs.menuWrapper, {})
  //     this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {})
  //   }
  // }
  // 7-6
}
</script>

<style lang="stylus" scoped>
@import "../../common/stylus/mixin.styl"
.goods
  display: flex
  position: absolute
  top: 174px
  bottom: 46px
  width:100%
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
          background-image: url('../../../static/img/decrease_1@2x.png')
        &.discount
          background-image: url('../../../static/img/discount_1@2x.png')
        &.guarantee
          background-image: url('../../../static/img/guarantee_1@2x.png')
        &.invoice
          background-image: url('../../../static/img/invoice_1@2x.png')
        &.special
          background-image: url('../../../static/img/special_1@2x.png')
      .text
        display: table-cell
        width: 56px
        vertical-align: middle
        font-size:12px
  .foods-wrapper
    flex: 1
    .title
      padding-left: 14px
      height: 26px
      line-height: 26px
      border-left: 2px solid #d9dde1
      font-size: 12px
      color: rgb(147,153,159)
      background: #f3f5f7
    .food-item
      display: flex
      margin: 18px
      padding-bottom:
      &:last-child
        margin-bottom: 0
        &:after
          display: none
      .icon
        flex: 0 0 57px
        margin-right: 10px
      .content
        flex: 1
        .name
          margin: 2px 0 8px 0
          height: 14px
          line-height: 14px
          font-size: 14px
          color: rgb(7,17,27)
        .desc, .extra
          line-height: 10px
          font-size: 10px
          color: rgb(147,153,159)
        .desc
          margin-bottom: 8px
        .extra
          &.count
            margin-right: 12px
        .price
          font-weight: 700
          line-height: 24px
          .now
            margin-right: 8px
            font-size: 14px
            color: rgb(240,20,20)
          .old
            text-decoration: line-through
            font-size: 10px
            color: rgb(147,153,159)
</style>
