<script setup>
import { ref, onMounted } from 'vue'

const visible = ref(false)

onMounted(() => {
  setTimeout(() => { visible.value = true }, 1000)
})

function close() {
  visible.value = false
}
</script>

<template>
  <Transition name="cookie">
    <div v-if="visible" class="cookie-wrapper">
      <div class="cookie-bar">
        <p class="cookie-bar__text">
          Мы используем <span class="cookie-bar__accent">cookies</span>, чтобы сайт был лучше
        </p>

        <img
          class="cookie-bar__duck"
          src="./cookie-duck.svg"
          alt=""
          aria-hidden="true"
          width="87"
          height="75"
        />

        <button class="cookie-bar__btn" @click="close">Хорошо</button>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
/* Requires Onest font:
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link href="https://fonts.googleapis.com/css2?family=Onest:wght@400&display=swap" rel="stylesheet">
*/

.cookie-wrapper {
  position: fixed;
  bottom: 8px;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  padding: 0 8px;
  z-index: 9999;
  pointer-events: none;
}

.cookie-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 22px;
  width: 100%;
  max-width: 1350px;
  height: 46px;
  background: #282931;
  border-radius: 12px;
  overflow: visible;
  pointer-events: all;
}

.cookie-bar__text {
  margin: 0;
  font-family: 'Onest', sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 1.4;
  color: #f1f1f3;
  letter-spacing: -0.02px;
  white-space: nowrap;
}

.cookie-bar__accent {
  color: #aab2ff;
}

/* Duck overflows 29px above the bar — align-self: flex-end places
   its bottom flush with the bar bottom, so the top protrudes upward */
.cookie-bar__duck {
  align-self: flex-end;
  flex-shrink: 0;
  display: block;
}

.cookie-bar__btn {
  flex-shrink: 0;
  width: 84px;
  height: 26px;
  padding: 0;
  background: #606fff;
  border: none;
  border-radius: 8px;
  font-family: 'Onest', sans-serif;
  font-size: 14px;
  font-weight: 400;
  color: #fff;
  cursor: pointer;
  transition: background 0.15s;
}

.cookie-bar__btn:hover {
  background: #7b8fff;
}

/* Transition */
.cookie-enter-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}
.cookie-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.cookie-enter-from,
.cookie-leave-to {
  opacity: 0;
  transform: translateY(16px);
  filter: blur(8px);
}
</style>
