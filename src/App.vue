<script setup>
import { onMounted, ref } from 'vue';

const h1 = ref('Jeg er en string')
const show = ref()

onMounted(() => {
  hey([...h1.value])
})

const hey = (letterArray) => {

  show.value.innerHTML = '';

  [...letterArray].forEach(letter => {
    const div = document.createElement('div')
    const span1 = document.createElement('span')
    const span2 = document.createElement('span')
    span1.innerHTML = letter === ' ' ? '&nbsp' : letter
    span2.innerHTML = letter === ' ' ? '&nbsp' : letter
    div.classList.add('flex')
    div.appendChild(span1)
    div.appendChild(span2)
    show.value.appendChild(div)
  })
}


</script>

<template>
  <input type="text" v-model="h1" @keyup="hey(h1)" />

  <div class="show" ref="show"></div>
</template>

<style  lang="scss">
body {
  display: flex;
  height: 100dvh;
  align-items: center;
  justify-content: center;
}

.flex {
  display: flex;
  flex-direction: column;
}

.show {
  font-weight: 900;
  display: flex;
  flex-direction: row;
  overflow: hidden;
  position: relative;
  font-size: 90px;
  line-height: 1.2;

  span {
    display: inline-block;
    height: 100%;

    &:nth-child(2) {
      position: absolute;
      top: 100%
    }
  }
}

.flex {
  animation: up 2.5s var(--direction, forwards) cubic-bezier(1, 0, 0, 1) infinite;

  &:nth-child(even) {
    --direction: reverse;
  }
}

@keyframes up {
  0% {
    transform: translateY(0%);
  }

  100% {
    transform: translateY(-100%);
  }
}
</style>
