<template>
  <div class="app">
      <v-header></v-header>

      <div class="tab">
          <div class="tab-item">
              <router-link to="/app/goods">商品</router-link>
          </div>
          <div class="tab-item">
              <router-link to="/app/ratings">评论</router-link>
          </div>
          <div class="tab-item">
              <router-link to="/app/seller">商家</router-link>
          </div>
      </div>

      <transition>
          <router-view></router-view>
      </transition>

  </div>
</template>

<script>
import Header from '@/components/header/header'

export default {
    components: {
        'v-header': Header
    }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.app
    .tab
        display flex
        witdh   100%
        height  40px
        line-height 40px
        border-bottom 1px solid rgba(7,17,27,0.1)
        .tab-item
            flex 1
            text-align center
            & > a
                display: block
                text-decoration none
                font-size: 14px
                color: rgb(77, 85, 93)
                &.active
                    color: rgb(240, 20, 20)
</style>
