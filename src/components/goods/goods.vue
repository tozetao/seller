<template>
    <div class="goods">
        <div class="menu-wrapper">
            <ul>
                <li class="menu-item" v-for="(item, index) in goods" :key="index">
                    <span class="icon" v-show="item.type>0" :class="iconMap[item.type]"></span>
                </li>
            </ul>
        </div>
        <div class="foods-wrapper"></div>
    </div>
</template>

<script type="text/ecmascript-6">
export default {
    data () {
        return {
            goods: []
        }
    },
    props: {
        seller: {
            type: Object
        }
    },
    created () {
        this.$nextTick(() => {
            this.$http.get('app/goods').then((response) => {
                response = response.body

                if (response.errno === 0) {
                    this.goods = response.data
                    console.log(this.goods)
                }
            })
            this.iconMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special']
        })
    }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.goods
    display: flex
    position: absolute;
    top:179px
    bottom 46px
    width:100%
    .menu-wrapper
        flex 0 0 80px
        width: 80px
        background #f3f5f7
        .menu-item
            display: table
            height:54px
            width:56px
            line-height:14px
            .icon
                vertical-align top
                display inline-block
                width 12px
                height: 12px
                background-repeat no-repeat
                background-size 12px 12px
                margin-right 4px
                &.decrease
                    bg-image('decrease_1')
                &.discount
                    bg-image('discount_1')
                &.invoice
                    bg-image('invoice_1')
                &.guarantee
                    bg-image('guarantee_1')
    .foods-wrapper
        flex: 1
</style>
