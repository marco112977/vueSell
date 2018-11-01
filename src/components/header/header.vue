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
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bullentin-wrapper" @click="showDetail">
      <span class="bullentin-title"></span><span class="bullentin-text">{{ seller.bulletin }}</span>
      <i class="icon icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>

    <transition name="fade">
    <div class="detail" v-show="detailShow">
      <div class="detail-wrapper">
        <div class="detail-main">
          <div class="name">{{ seller.name }}</div>
          <div class="star-wrapper">
            <star :size="48" :score="seller.score"></star>
          </div>
         <div class="title">
           <div class="line"></div>
           <div class="text">优惠信息</div>
           <div class="line"></div>
         </div>
         <ul v-if="seller.supports" class="supports">
          <li class="support-item" v-for="support in seller.supports">
            <span class="icon" :class="classMap[support.type]"></span>
            <span class="text">{{ support.description }}</span>
          </li>
         </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>

          <div class="bulletin">
            <div class="text">{{ seller.bulletin }}</div>
          </div>

        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon icon-close"></i>
      </div>
    </div>
    </transition>

  </div>

</template>

<script>
  import star from '../../components/star/star'
  export default {
    name: 'Header',
    props: {
      seller: {
        type: Object
      }
    },
    components: {
      star
    },
    created () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    },
    data () {
      return {
        detailShow: false
      }
    },
    methods: {
      showDetail () {
        this.detailShow =  true
      },
      hideDetail () {
        this.detailShow =  false
      }
    },

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
        vertical-align:middle
      .bullentin-text
        font-size:10px;
        margin:0 4px
      .icon-keyboard_arrow_right
        position:absolute
        right:12px
        font-size: 10px
        top: 0px
    .background
      position:absolute
      top:0
      left:0
      right:0
      z-index:-1
      width: 100%
      height:100%
      filter:blur(10px)
    .detail
      position: fixed
      z-index: 1000
      top:0
      left:0
      height: 100%
      width: 100%
      background : rgba(7,17,27,0.5)
      overflow :auto
      backdrop-filter: blur(10px)
      &.fade-enter-active, .fade-leave-active
        transition: opacity .5s;
      &.fade-enter, .fade-leave
        opacity: 0;
        background :rgba(7,17,27,0)
      .detail-wrapper
        min-height: 100%
        width: 100%

        .detail-main
          margin-top:64px
          padding-bottom: 64px
          .name
            font-size:16px
            line-height: 16px
            text-align:center
          .star-wrapper
            text-align:center
            margin:16px auto 28px
          .title
            display: flex
            width:80%
            margin:28px auto 24px
            .line
             flex :1
             border-bottom 1px solid rgba(255,255,255,0.2)
             position :relative
             top: -6px
            .text
              text-align: center
              font-size: 14px
              font-weight:700
              padding:0 12px
          .supports
            width: 80%
            margin:0 auto
            .support-item
              padding:0 12px
              margin-bottom:12px
              font-size:0
              &:last-child
               margin-bottom :0
              .icon
                display :inline-block
                width:16px
                height:16px
                margin-right: 6px
                vertical-align: top
                background-size:16px 16px
                background-repeat:no-repeat
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.guarantee
                  bg-image('guarantee_2')
                &.invoice
                  bg-image('invoice_2')
                &.special
                  bg-image('special_2')
              .text
                font-size: 12px
                line-height:16px
          .bulletin
            margin:0 auto
            width: 80%
            font-size:12px
            line-height:24px
            font-weight:200
            .text
              padding:0 12px
      .detail-close
        margin: -128px auto 0;
        width:32px
        height:32px
        clear :both
        position:relative
        font-size: 32px
</style>
