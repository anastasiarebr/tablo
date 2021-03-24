<template>
<div class="body">
<div class="titles">
      <div class="title">
        <span>Поступающий</span>
        <span>№ стола</span>
      </div>
      <div class="title">
        <span>Поступающий</span>
        <span>№ стола</span>
      </div>
      <div class="title">
        <span>Поступающий</span>
        <span>№ стола</span>
      </div>
</div>
  <div class="main">
    <div class="column">
      <div class="column-items" >
        <div class="column-item " v-for="person in people" :key="person.id" :class="(person.id % 2 !== 0) ? 'bgdblue' : ''">
          <div class="person">{{person.id}}</div>
          <div class="arrow">
              <svg
            width="46"
            height="46"
            viewBox="0 0 46 46"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g clip-path="url(#clip0)">
              <path
                d="M2.76485 26.2289C2.95308 26.2594 3.14356 26.2735 3.33414 26.271L35.7862 26.271L35.0786 26.6002C34.3869 26.9276 33.7577 27.3731 33.219 27.9167L24.1186 37.0171C22.9201 38.1612 22.7187 40.0017 23.6414 41.378C24.7153 42.8446 26.7747 43.163 28.2414 42.0891C28.3599 42.0023 28.4725 41.9077 28.5783 41.8059L45.0347 25.3495C46.3208 24.0649 46.3219 21.981 45.0373 20.6949C45.0365 20.6941 45.0355 20.6932 45.0347 20.6923L28.5783 4.23595C27.2912 2.95246 25.2073 2.95534 23.9237 4.24243C23.8227 4.34374 23.7284 4.45153 23.6414 4.56508C22.7187 5.94135 22.9201 7.78189 24.1186 8.92602L33.2026 18.0429C33.6855 18.5263 34.2407 18.9316 34.8482 19.2442L35.8356 19.6885L3.51527 19.6885C1.83394 19.6261 0.358829 20.8005 0.0429688 22.4532C-0.248001 24.2474 0.970596 25.9378 2.76485 26.2289Z"
                fill="#1E9EE6"
              />
            </g>
            <defs>
              <clipPath id="clip0">
                <rect
                  width="46"
                  height="46"
                  fill="white"
                  transform="translate(46 46) rotate(-180)"
                />
              </clipPath>
            </defs>
          </svg>
          </div>
          <div class="table">{{person.num}}</div>
        </div>
      </div>
    </div>
  </div>
  <transition name="fade">
    <div v-if="addNewItem === 1" class="newItem">
      Абитуриент с талоном <span>{{newItem.id}}</span> подойдите к столу <span>{{newItem.num}}</span>
  </div>
  </transition>
  <button @click="add">Add</button>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup () {
    const people = ref([
      {
        id: 1,
        num: 4
      },
      {
        id: 2,
        num: 6
      },
      {
        id: 3,
        num: 1
      },
      {
        id: 4,
        num: 9
      },
      {
        id: 5,
        num: 15
      },
      {
        id: 6,
        num: 8
      },
      {
        id: 7,
        num: 20
      }
    ])
    const newItem = { id: 10, num: 50 }
    const addNewItem = ref(0)
    const audio = new Audio(require('../sound/sound.mp3'))

    function add () {
      audio.play()
      addNewItem.value = 1
      setTimeout(() => {
        addNewItem.value = 0
        people.value.push(newItem)
      }, 2000)
    }

    return {
      people,
      add,
      newItem,
      addNewItem
    }
  }
}
</script>

<style lang="sass" scoped>
@import '@/sass/style'
</style>
