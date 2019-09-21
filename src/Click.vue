<style scoped>
.heart {
  width: 10px;
  height: 10px;
  opacity: 0;
  position: fixed;
  z-index: 999;
  background: #fff;
  transform: translateY(-50px) rotate(45deg) scale(1.5);
}

.heart:after,
.heart:before {
  content: "";
  width: inherit;
  height: inherit;
  background: inherit;
  border-radius: 50%;
  position: absolute;
}

.heart:after {
  top: -5px;
}

.heart:before {
  left: -5px;
}

.list-enter-active {
  transition: all 1.5s;
}

.list-enter {
  opacity: 1;
  transform: translateY(0px) rotate(45deg) scale(1);
}
</style>

<template>
  <transition-group name="list" tag="div">
    <div v-for="item in hearts" class="heart" :key="item" :style="item"/>
  </transition-group>
</template>

<script>
import { isMobile } from './utils'

export default {
  name: "heart",
  data() {
    return {
      hearts: [],
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      if(isMobile()) return console.log('mobile does not work')
      window.addEventListener('click', (event) => {
        this.hearts.push(`
          left: ${event.clientX - 5}px;
          top: ${event.clientY - 5}px;
          background: ${this.getColor()};
        `)
        setTimeout(() => {
          this.hearts.shift()
        }, 1500)
      })
    },
    getColor() {
      const random = () => Math.floor(Math.random() * 255)
      return `rgb(${random()}, ${random()}, ${random()})`
    },
  }
};
</script>
