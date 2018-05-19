<template>
    <div class="goods">
        <div class="menu-wrapper">
            <ul>
                <li class="menu-item" v-for="(item, index) in goods" :key="index">
                    <span class="text">
                        <span v-show="item.type>0" :class="iconMap[item.type]" class="icon"></span>{{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="foods-wrapper">
            <ul>
                <li class="food-list" v-for="(item, index) in goods" :key="index">
                    <h1 class="title">{{item.name}}</h1>
                    <ul>
                        <li v-for="(food, index) in item.foods" :key="index" class="food-item">
                            <div class="icon">
                                <img :src="food.icon" width="57">
                            </div>
                            <div class="content">
                                <h2 class="name">
                                    {{food.name}}
                                </h2>
                                <p class="desc">{{food.description}}</p>
                                <div class="extra">
                                    <span>月售{{food.sellCount}}份</span>
                                    <span>好评率{{food.rating}}%</span>
                                </div>
                                <div class="price">
                                    <span>${{food.price}}</span>
                                    <span v-show="food.oldPrice">${{food.oldPrice}}</span>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
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
    @import "../../common/stylus/mixin.styl"
.goods
    display: flex
    position: absolute;
    top:179px
    bottom 46px
    width:100%
    overflow: hidden
    .menu-wrapper
        flex 0 0 80px
        width: 80px
        background #f3f5f7
        .menu-item
            display: table
            height: 54px
            width: 56px
            line-height: 13px
            padding: 0 12px
            .text
                display: table-cell
                font-size:13px
                width:56px
                vertical-align middle
                border-bottom 1px solid rgba(7,17,27,0.1)
                .icon
                    display inline-block
                    vertical-align top
                    width 12px
                    height: 12px
                    background-repeat no-repeat
                    background-size 12px 12px
                    margin-right 2px
                    &.decrease
                        bg-image('decrease_3')
                    &.discount
                        bg-image('discount_3')
                    &.invoice
                        bg-image('invoice_3')
                    &.guarantee
                        bg-image('guarantee_3')
                    &.special
                        bg-image('special_3')
    .foods-wrapper
        flex: 1
        .title
            padding-left 14px
            height:26px
            line-height:26px
            border-left: 2px solid #d9dbe1
            font-size:12px
            color: rgb(147,153,159)
            background #f3f5f7
        .food-item
            display: flex
            margin:18px
            border-1px(rgba(7,17,27,0.1))
            padding-bottom: 18px
            &:last-child
                border-none()
                margin-bottom: 0
            .icon
                flex: 0 0 57px
                margin-right:10px

</style>
