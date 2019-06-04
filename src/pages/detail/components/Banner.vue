<template>
    <div>
        <div class="banner" @click="handeBannerClick">
            <img class="banner-img" :src='img'/>
            <div class="banner-info">
                <div class="banner-title">{{title}}</div>
                <div class="banner-number">
                    <span class="iconfont banner-icon">&#xe674;</span>
                    39
                </div>
            </div>
        </div>
        <FadeAnimation>
            <CommonGallary :imgs="gallaryImgs" v-show="showGallary" @close="handeGallaryClose"></CommonGallary>
        </FadeAnimation>
    </div>
</template>

<script>
import CommonGallary from '../../../common/gallary/Gallary'
import FadeAnimation from '../../../common/fade/Fade'
export default {
  name: 'DetailBanner',
  components: {
    CommonGallary,
    FadeAnimation
  },
  props: {
    title: String,
    img: String,
    gallaryImgs: Array
  },
  data () {
    return {
      showGallary: false
    }
  },
  methods: {
    handeBannerClick () {
      this.showGallary = true
    },
    handeGallaryClose () {
      this.showGallary = false
    }
  }
}
</script>

<style lang="stylus" scoped>
    .banner
        position: relative
        height: 0
        padding-bottom: 50%
        background: red
        overflow: hidden
        .banner-img
            width: 100%
        .banner-info
            display: flex
            position: absolute
            left: 0
            right: 0
            bottom: 0
            line-height: .6rem
            color: #fff
            background-image: linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,.8))
            .banner-title
                flex: 1
                font-size: .32rem
                padding: 0 .2rem
            .banner-number
                padding: 0 .4rem
                height: .4rem
                line-height: .4rem
                border-radius: .2rem
                background: rgba(0,0,0,.8)
                .banner-icon
                    font-size: .3rem
</style>
