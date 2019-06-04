<template>
    <ul class="list">
        <li class="item"
            v-for="item of letters"
            :key="item"
            :ref="item"
            @click="handleLetterClick"
            @touchstart="handleTouchStart"
            @touchmove="handleTouchMove"
            @touchend="handleTouchEnd"
        >
            {{item}}
        </li>
    </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  data () {
    return {
      touchFlag: false,
      startY: 0,
      timer: null
    }
  },
  computed: {
    letters () {
      return Object.keys(this.cities)
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchFlag = true
    },
    handleTouchEnd () {
      this.touchFlag = false
    },
    handleTouchMove (e) {
      if (this.touchFlag) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 83
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index <= this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'
    .list
        position: absolute
        top: 1.58rem
        right: 0
        bottom: 0
        width: .4rem
        display: flex
        flex-direction: column
        justify-content: center
        text-align: center
        .item
            line-height: .4rem
            color: $bgColor
</style>
