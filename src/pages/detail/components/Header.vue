<template>
    <div>
        <router-link tag="div" to="/" class="header-abs" v-show="showAbs">
            <div class="iconfont header-abs-back">&#xe624;</div>
        </router-link>
        <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
            <router-link to='/'>
                <div class="iconfont header-fixed-back">&#xe624;</div>
            </router-link>
            景点详情
        </div>
    </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll () {
      let scrollTop = document.documentElement.scrollTop
      this.showAbs = true
      if (scrollTop > 60) {
        this.showAbs = false
      }
      if (scrollTop > 60 && scrollTop < 140) {
        const opacity = scrollTop / 140
        this.opacityStyle = { opacity }
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'
    .header-abs
        position: absolute
        background: rgba(0,0,0,.8)
        width: .6rem
        height: .6rem
        border-radius: 50%
        left: .2rem
        top: .2rem
        line-height .6rem
        text-align: center
        .header-abs-back
            color: #fff
            font-size: .4rem
    .header-fixed
        position: fixed
        z-index: 2
        top: 0
        left: 0
        right: 0
        height: $headerHeight
        line-height: $headerHeight
        background: $bgColor
        color: #fff
        overflow: hidden
        text-align: center
        .header-fixed-back
            position: absolute
            top: 0
            left: 0
            color: #fff
            width: .64rem
            font-size: .4rem
</style>
