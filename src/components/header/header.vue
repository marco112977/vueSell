<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar"/>
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="description">
          {{ seller.description }}/{{ seller.deliveryTime }}分钟到达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bullentin-wrapper">
      <span class="bullentin-title"></span><span class="bullentin-text">{{ seller.bulletin }}</span>
      <i class="icon icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
  </div>

</template>

<script>
  export default {
    name: 'Header',
    props: {
      seller: {
        type: Object
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    },
    data () {
      return {}
    }
  }

</script>
<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin"
  .header
    position:relative
    color: #fff
    overflow: hidden
    background:rgba(7,17,27,0.5)
    .content-wrapper
      padding: 24px 12px 18px 24px
      position:relative
      font-size: 0
      .avatar
        display:inline-block
        vertical-align:top
        img
          border-radius :2px
      .content
        display: inline-block
        margin-left: 16px
        .title
          margin:2px 0 8px 0
          .brand
            width:30px
            height:18px
            display: inline-block;
            bg-image('brand')
            background-size :30px 18px
            background-repeat: no-repeat
            vertical-align: top
          .name
            font-size:16px
            font-weight:bold
            line-height 18px
            margin-left:6px

        .description
          margin-bottom: 10px
          font-size:12px
          line-height:12px
        .support
          .icon
            display:inline-block
            width:12px
            height:12px
            vertical-align:top
            margin-right:4px
            background-size:12px 12px
            background-repeat:no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            font-size: 10px
            line-height: 12px
      .support-count
        position:absolute;
        right:12px
        bottom:18px
        padding:0 8px
        height:24px
        line-height:24px
        border-radius 14px
        background:rgba(0,0,0,0.2)
        .count
          font-size: 10px
        .icon-keyboard_arrow_right
          line-height 24px;
          font-size 10px
          margin-left:2px
    .bullentin-wrapper
      position:relative
      height 28px
      line-height 28px
      padding:0 22px 0 12px
      white-space:nowrap
      overflow: hidden
      text-overflow ellipsis
      background:rgba(7,17,27,0.2)
      .bullentin-title
        display:inline-block
        width:22px
        height:12px
        bg-image('bulletin')
        background-size:22px 12px
        background-repeat:no-repeat
      .bullentin-title
        font-size:10px;
        margin:0 4px
      .icon-keyboard_arrow_right
        position:absolute
        right:12px
        font-size:10px
        top:0px
    .background
      position:absolute
      top:0
      left:0
      right:0
      z-index:-1
      width: 100%
      height:100%
      filter:blur(10px)
</style>
