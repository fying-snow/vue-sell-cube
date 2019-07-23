<template>
  <div class="goods">
    <!--    左栏宽度固定-->
    <div class="menu-wrapper">
      <ul>
        <li v-for="(item,index) in goods" :key="index" class="menu-item">
          <span class="text border-1px">
            <span v-if="item.type > 0" class="icon">
              <support-ico :size=3 :type="item.type"></support-ico>
            </span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <!--    右栏根据屏宽缩放-->
    <div class="food-wrapper"></div>
  </div>
</template>

<script>
  import { getGoods } from '../../api'
  import SupportIco from '../support-ico/support-ico'

  export default {
    name: 'goods',
    props: {
      seller: {
        type: Object,
      }
    },
    data () {
      return {
        goods: []
      }
    },
    created () {
      this._getGoods()
    },
    methods: {
      _getGoods () {
        getGoods().then((goods) => {
          this.goods = goods
        })
      }
    },
    components: {
      SupportIco
    },
  }
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin.styl"
  .goods
    display: flex
    position: absolute
    top: 0
    bottom: 46px
    width: 100%
    //隐藏超过部分，不显示滚动条
    overflow: hidden

    .menu-wrapper
      //flex: 等分，内容不足缩放，占位
      flex: 0 0 80px
      // 不写的话，安卓手机有问题
      width: 80px
      background: #f3f5f7
      .menu-item
        //方便垂直居中 (可能是单行/多行)
        display: table
        height: 54px
        width: 56px
        padding: 0 12px
        line-height: 14px
        .icon
          display: inline-block
        .text
          display: table-cell
          width: 56px
          vertical-align: middle
          border-1px(rgba(7, 17, 27, 0.1))
          font-size: 12px
    .food-wrapper
      flex: 1
</style>
