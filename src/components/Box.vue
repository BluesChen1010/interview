<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const showAnimate = (n, act) => {
  if (n === 1 || n === 3) {
    return act === 3
  } else if (n === 2) {
    return act === 2
  }
  return false
}

const showCircle = (n, act) => {
  if (n === 1 || n === 3) {
    return act === 1 || act === 3
  }
  return false
}

const type = ref('一般模式')
const changeType = () => {
  if (type.value === '一般模式') type.value = '特殊模式'
  else type.value = '一般模式'
  
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <button type="button" @click="changeType()">{{ type }}</button>
  <div class="normal-card" v-if="type === '一般模式'">
    <p>題目: 方塊寬度200px ,題目動畫向右500px, 所以最左邊球體不會完全消失</p>
    <ul v-for="n in 3">
      <li :class="{'move': showAnimate(n, act)}" v-for="act in 3">
        <div v-if="showCircle(n, act)" class="circle normal"></div>
      </li>
    </ul>
  </div>
  <div class="special-card" v-if="type === '特殊模式'">
    <ul v-for="n in 3">
      <li :class="{'move': showAnimate(n, act)}" v-for="act in 3">
        <div v-if="showCircle(n, act)"  class="circle special"></div>
      </li>
    </ul>
  </div>
</template>

<style lang="sass" scoped>
.circle
  z-index: 2
  position: absolute
  width: 30px
  height: 30px
  border-radius: 50%
  background-color: #A5F12B
  &.normal
    animation-duration: 7s
    animation-iteration-count: infinite
    animation-name: circle
  &.special
    animation-name: moveTo
    animation-duration: 5s
    animation-iteration-count: infinite

.normal-card
  padding: 0
  overflow: hidden
  position: relative
  display: flex
  justify-items: center
  align-items: center
  flex-direction: column
  ul
    height: auto
    width: auto
    margin: 0
    padding: 0
    display: flex
    justify-items: center
    align-items: center
    li
      position: relative
      display: flex
      justify-content: center
      align-items: center
      margin: 5px
      width: 200px
      height: 100px
      border: black solid 2px
      background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%)
      list-style: none
      &.move
        animation-name: opacityColor
        animation-duration: 2s
        animation-iteration-count: infinite
.special-card
  padding: 0
  overflow: hidden
  position: relative
  display: flex
  justify-items: center
  align-items: center
  flex-direction: column
  ul
    height: auto
    width: auto
    margin: 0
    padding: 0
    display: flex
    justify-items: center
    align-items: center
    li
      display: flex
      justify-content: center
      align-items: center
      margin: 5px
      width: 200px
      height: 100px
      border: black solid 2px
      background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%)
      list-style: none
    &:nth-child(1)
      li
        &:nth-child(1)
          .circle
            right: 515px
            bottom: 265px
        &:nth-child(3)
          .circle
            right: 90px
            bottom: 265px
    &:nth-child(3)
      li
        &:nth-child(1)
          .circle
            right: 515px
            bottom: 40px
        &:nth-child(3)
          .circle
            right: 90px
            bottom: 40px

        
      &.move
        animation-name: opacityColor
        animation-duration: 2s
        animation-iteration-count: infinite

@keyframes circle
  from
    left: 100px
  to
    left: 500px


@keyframes moveTo
  to
    right: 0px
    bottom: 0px


@keyframes opacityColor
  0%
    opacity: 60%
  25%
    opacity: 100%
  50%
    opacity: 60%
  75%
    opacity: 100%
  100%
    opacity: 60%
</style>
