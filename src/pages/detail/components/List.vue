<template>
    <div>
        <div class="item border-bottom" v-for="(item,index) of list" :key="index">
            <div class="item-title">
                <span class="item-title-icon"></span>
                {{item.title}}
            </div>
            <div v-if="item.children" class="item-children">
                <DetailList :list="item.children"></DetailList>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'DetailList',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
    .item-children
        padding: 0 .2rem
    .item-title
        height: .7rem
        line-height: .7rem
        padding: 0 .2rem
        .item-title-icon
            position: relative
            top: .1rem
            display: inline-block
            width: .36rem
            height: .36rem
            background: url(//s.qunarzz.com/piao/image/touch/sight/detail.png) 0 -.45rem no-repeat
            margin-right: .1rem
            background-size: .4rem 3rem
</style>
