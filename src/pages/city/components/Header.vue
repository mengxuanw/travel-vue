<template>
    <div class="header">
        城市选择
        <router-link to='/'>
            <div class="iconfont header-back">&#xe624;</div>
        </router-link>
    </div>
</template>

<script>
export default {
  name: 'CityHeader'
}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'
    .header
        position: relative
        height: $headerHeight
        line-height: $headerHeight
        background: $bgColor
        color: #fff
        overflow: hidden
        text-align: center
        .header-back
            position: absolute
            top: 0
            left: 0
            color: #fff
            width: .64rem
            font-size: .4rem
</style>
