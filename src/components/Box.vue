<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>
  <button type="button" @click="count++">次數: {{ count }}</button>
  <div class="card">
    <ul v-for="n in 3">
      <li v-for="n in 3"></li>
    </ul>
  </div>
</template>

<style lang="sass" scoped>
.circle
  width: 30px
  height: 30px
  background-color: #A5F12B
.card
  position: relative
  display: flex
  justify-items: center
  align-items: center
  flex-direction: column
  ul
    margin: 0
    display: flex
    justify-items: center
    align-items: center
    li
      margin: 5px
      width: 200px
      height: 100px
      border: black solid 2px
      background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%)
      list-style: none
</style>
