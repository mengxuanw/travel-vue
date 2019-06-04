<template>
    <div>
        <div class="serach">
            <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音"/>
        </div>
        <div class="search-content" ref="content" v-show="keyword">
            <ul>
                <li @click="handleCityClick(item.name)" class="search-item border-bottom" v-for="item in list" :key="item.id">{{item.name}}</li>
                <li class="search-item border-bottom" v-show="hasNoData">没有找到匹配数据</li>
            </ul>
        </div>
    </div>
</template>

<script>
import BScroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  props: {
    cities: Object
  },
  mounted () {
    this.scroll = new BScroll(this.$refs.content)
  },
  methods: {
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations([
      'changeCity'
    ])
  },
  computed: {
    hasNoData () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.name.indexOf(this.keyword) > -1 ||
              value.spell.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  }
}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'
    .serach
        background: $bgColor
        height: .8rem
        line-height: .8rem
        padding: 0 .1rem
        .search-input
            box-sizing: border-box
            width: 100%
            height: .62rem
            line-height: .62rem
            padding: 0 .1rem
            border-radius: .06rem
            color: #666
    .search-content
        z-index: 1
        position: absolute
        background: #eee
        top: 1.67rem
        left: 0
        right: 0
        bottom: 0
        overflow: hidden
        .search-item
            line-height: .62rem
            padding-left: .2rem
            background: #fff
            color: #666
</style>
