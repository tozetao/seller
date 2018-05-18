<template>
    <div class="goods">
        <div class="menu-wrapper"></div>
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
    .foods-wrapper
        flex: 1
</style>
