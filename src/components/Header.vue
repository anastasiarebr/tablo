<template>
  <div class="header">
    <img src="../assets/logo.png" alt="logo" class="logo" />
    <div class="date-wraper">
      <div class="date-wraper time">{{ hours }}:{{minutes}}</div>
      <div class="date-wraper date">{{ date }}</div>
    </div>
  </div>
</template>

<script>
import { onMounted, onBeforeUnmount, ref } from 'vue'
import { getZeroPad } from './composables/Filters'
export default {
  setup () {
    const hours = ref('')
    const minutes = ref('')
    const seconds = ref('')
    const date = ref('')
    let timer = ''

    function updateTime () {
      const Data = new Date()
      hours.value = Data.getHours()
      minutes.value = Data.getMinutes()
      seconds.value = Data.getSeconds()
      if (hours.value < 10) {
        hours.value = '0' + hours.value
      }
      if (minutes.value < 10) {
        minutes.value = '0' + minutes.value
      }
      date.value = getZeroPad(Data.getDate()) + '.' + getZeroPad(Data.getMonth() + 1) + '.' + getZeroPad(Data.getFullYear())
    }

    onMounted(() => {
      timer = setInterval(updateTime, 1000)
    })
    onBeforeUnmount(() => {
      clearInterval(timer)
    })

    return {
      hours,
      minutes,
      seconds,
      date,
      timer
    }
  }
}
</script>

<style lang="sass" scoped>
@import '@/sass/style'
</style>
