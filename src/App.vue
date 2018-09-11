<template>
  <div id="app">
    <v-header :seller="seller"/>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link tag="li" to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link tag="li" to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link tag="li" to="/seller">商家</router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import header from './components/header/header'

export default {
  data () {
    return {
      seller: {}
    }
  },
  components: {
    'v-header': header
  },
  created () {
    this.$axios.get('/api/seller').then((res) => {
      if (res.status === 200) {
        this.seller = res.data.data
      }
    })
  }
}
</script>

<style lang="stylus" scoped>
@import "./common/stylus/mixin.styl";
@import "./common/stylus/base.styl";
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    // border-bottom:1px solid rgba(7,17,27,0.1)
    // position:relative
    // &:after
    //   display:block
    //   position:absolute
    //   left: 0
    //   bottom: 0
    //   width: 100%
    //   border-top: 1px solid rgba(7,17,27,0.1)
    //   content: ''
    .tab-item
      flex: 1
      text-align: center
      & > li
        display:block
        font-size: 14px
        color: rgb(77,85,93)
        &.active
          color: rgb(240,20,20)
</style>
