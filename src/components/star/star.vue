/**
 * @author GQ
 * @created 2019-06-20 09:23
 * @modified 2019-06-27 13:33
 * @Description: starTest.vue 该组件是用来显示一排评分星星的 ⭐️
*/

<template>
    <div class="starList" :class="starType">
      <span v-for="(itemClass, index) in itemClasses" :key="index" class="singleStar" :class="itemClass">️</span>
    </div>
</template>

<script>

  const LENGTH = 5;
  const HALF = 'half';
  const ON = 'on';
  const OFF = 'off';

  export default {
    name: 'starTest',
    props: {
      size: {
        type: Number,
      },
      score: {
        type: Number,
      }
    },
    computed: {
      starType() {
        return 'star-' + this.size;
      },
      itemClasses() {
        let starItems = [];
        let newScore = Math.floor(this.score * 2) / 2;
        let hasDecimal = newScore % 1 !== 0;
        let integer = Math.floor(newScore);

        for (let i = 0; i < integer && i < LENGTH; i++) {
          starItems.push(ON);
        }
        if (hasDecimal) {
          starItems.push(HALF);
        }
        while (starItems.length < LENGTH) {
          starItems.push(OFF);
        }
        // 别忘了return
        return starItems;
      }
    },
  };
</script>

<style scoped lang="stylus">
  @import '~common/stylus/mixin';
  .starList
    font-size: 0
    .singleStar
      display: inline-block
      background-repeat: no-repeat
    &.star-48
      .singleStar
        width: 20px
        height: 20px
        margin-right: 4px
        background-size: 20px 20px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star48_on')
        &.off
          bg-image('star48_off')
        &.half
          bg-image('star48_half')
    &.star-36
      .singleStar
        width: 15px
        height: 15px
        margin-right: 6px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star36_on')
        &.half
          bg-image('star36_half')
        &.off
          bg-image('star36_off')
    &.star-24
      .singleStar
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star24_on')
        &.half
          bg-image('star24_half')
        &.off
          bg-image('star24_off')
</style>
