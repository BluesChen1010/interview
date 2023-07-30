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

const type = ref('一般模式')
const changeType = () => {
  if (type.value === '一般模式') type.value = '特殊模式'
  else type.value = '一般模式'
  
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <button type="button" @click="changeType()">{{ type }}</button>
  <div class="card">
    <ul v-for="n in 3">
      <li :class="{'move': showAnimate(n, act)}" v-for="act in 3">
        <div class="circle"></div>
      </li>
    </ul>
  </div>
</template>

<style lang="sass" scoped>
.circle
  z-index: 2
  position: absolute
  top: 40px
  animation-name: circle
  animation-duration: 7s
  animation-iteration-count: infinite
  width: 30px
  height: 30px
  border-radius: 50%
  background-color: #A5F12B
.card
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

@keyframes circle
  from
    left: 0
  to
    left: 700px


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
