<template>
  <div class="tab">
    <!--       todo 2019-07-02 10:37 ref?-->
    <cube-tab-bar
      v-model="selectedLabel"
      show-slider
      :data="tabs"
      :useTransition=false
      ref="tabBar"
      class="border-bottom-1px"
    >
    </cube-tab-bar>
    <div class="slide-wrapper">
      <cube-slide
        :loop=false
        :auto-play=false
        :show-dots=false
        :initial-index="index"
        :options="slideOptions"
        ref="slide"
        @change="onChange"
        @scroll="onScroll"
      >
        <cube-slide-item v-for="(tab, index) in tabs" :key="index">
          <component :is="tab.component" :data="tab.data"></component>
        </cube-slide-item>
      </cube-slide>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'tab',
    props: {
      tabs: {
        type: Array,
        default() {
          return []
        },
      },
      initialIndex: {
        type: Number,
        default: 0
      }
    },
    data () {
      return {
        index: this.initialIndex,
        slideOptions: {
          listenScroll: true,
          probeType: 3,
          // 不监听竖向滚动 ？
          directionLockThreshold: 0
        }
      }
    },
    computed: {
      selectedLabel: {
        get() {
          return this.tabs[this.index].label
        },
        set(newVal) {
          //findIndex找到符合（函数）条件的第一个index
          this.index = this.tabs.findIndex((value) => {
            return value.label === newVal
          })
        }
      }
    },
    methods: {
      onChange(current) {
        this.index = current
      },
      // 监听slide滑动，设定tab下划线滑动
      onScroll(pos) {
        // console.log(pos.x) 负值
        const slideWidth = this.$refs.slide.slide.scrollerWidth
        const tabBarWidth = this.$refs.tabBar.$el.clientWidth
        // console.log("slideWidth", slideWidth, ", tabBarWidth: ", tabBarWidth)
        // slideWidth是多个slide的总宽，tabBarWidth等于屏幕宽度
        const transform = -pos.x / slideWidth * tabBarWidth
        this.$refs.tabBar.setSliderTransform(transform)
      }
    },
  }
</script>

<style lang="stylus" scoped>
  @import "~common/stylus/variable"

  .tab
    display: flex
    flex-direction: column
    height: 100%
    >>> .cube-tab
      padding: 10px 0
    .slide-wrapper
      flex: 1
      overflow: hidden
</style>
