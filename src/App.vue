<script setup>
import CookieBanner from '../CookieBanner.vue'
import LessonMaterials from '../LessonMaterials.vue'
</script>

<template>
  <div class="preview-bg">
    <LessonMaterials />
  </div>
  <CookieBanner />
</template>

<style scoped>
.preview-bg {
  min-height: 100vh;
  background: #f0f0f2;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
