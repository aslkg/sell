<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}} / {{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" @click="showDetail" class="support-count">
        <span class="count">{{ seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right">&nbsp;&gt;</i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right">&nbsp;&gt;</i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%" alt="">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
        </div>
      </div>
      <div class="detail-close">×</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      this.detailShow = true
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  }
}
</script>

<style lang="stylus" scoped>
.header
  position:relative
  overflow: hidden
  color: #fff
  background:rgba(7.17.27.0.5)
  .content-wrapper
    position:relative
    padding:24px 12px 18px 24px
    font-size:0
    .avatar
      display: inline-block
      vertical-align: top
      img
        border-radius: 2px
    .content
      display: inline-block
      margin-left:16px
      .title
        margin:2px 0 8px 0
        .brand
          display:inline-block
          vertical-align: top
          width: 30px
          height:18px
          background-image: url('../../../static/img/brand@2x.png')
          background-size: 30px 18px
          background-repeat:no-repeat
        .name
          margin-left: 6px
          font-size : 16px
          line-height: 18px
          font-weight: bold
      .description
        margin-bottom: 10px
        line-height: 12px
        font-size:12px
      .support
        .icon
          display: inline-block
          vertical-align: top
          width: 12px
          height: 12px
          margin-right: 4px
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
          line-height: 12px
          font-size:10px
    .support-count
      position:absolute
      right: 12px
      bottom: 14px
      padding: 0 8px
      height: 24px
      line-height: 24px
      border-radius: 14px
      background: rgba(0,0,0,0.2)
      text-align: center
      .count
        vertical-align: top
        font-size: 10px
      .icon-keyboard_arrow_right
        line-height: 24px
        margin-left: 2px
        font-size: 10px
  .bulletin-wrapper
    position:relative
    height: 28px
    line-height: 28px
    padding: 0 22px 0 12px
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background:rgba(7,17,27,0.2)
    .bulletin-title
      display: inline-block
      vertical-align: top
      margin-top: 8px
      width: 22px
      height: 12px
      background-image: url('../../../static/img/bulletin@2x.png')
      background-size:22px 12px
      background-repeat: no-repeat
    .bulletin-text
      margin: 0 4px
      font-size: 10px
    .icon-keyboard_arrow_right
      position:absolute
      font-size: 10px
      right: 12px
      top: 2px
  .background
    position:absolute
    top:0
    left:0
    width: 100%
    height:100%
    z-index: -1
    filter:blur(10px)
  .detail
    position:fixed
    z-index:100
    top:0
    left:0
    width:100%
    height 100%
    overflow:auto
    background:rgba(7,17,27,0.8)
    .detail-wrapper
      min-height: 100%
      width:100%
      .detail-main
        margin-top: 64px
        padding-bottom: 64px
        .name
          line-height: 16px
          text-align: center
          font-size: 16px
          font-weight: 700
    .detail-close
      position:relative
      width: 32px
      height: 32px
      margin: -64px auto 0 auto
      clear:both
      font-size: 32px
</style>
