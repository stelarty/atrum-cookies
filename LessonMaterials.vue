<script setup>
import { ref, computed } from 'vue'

const text = ref('')
const saved = ref(false)

const links = computed(() => {
  const lines = text.value.split('\n')
  const result = []

  for (let i = 0; i < lines.length; i++) {
    const line = lines[i].trim()
    if (!line) continue

    if (/^https?:\/\/\S+$/.test(line)) {
      const prev = i > 0 ? lines[i - 1].trim() : ''
      const label = prev && !/^https?:\/\//.test(prev)
        ? prev.toUpperCase()
        : extractDomain(line)
      result.push({ label, url: line })
    }
  }
  return result
})

function extractDomain(url) {
  try { return new URL(url).hostname.toUpperCase() }
  catch { return 'ССЫЛКА' }
}

function save() {
  if (links.value.length) saved.value = true
}

function reset() {
  saved.value = false
  text.value = ''
}
</script>

<template>
  <div class="card">
    <h2 class="card__title">Материалы урока</h2>

    <button class="card__upload-btn">Добавить файл</button>
    <p class="card__empty-files">Материалов пока нет</p>

    <Transition name="slide" mode="out-in">

      <!-- View mode -->
      <ul v-if="saved" key="view" class="link-list">
        <li v-for="(item, i) in links" :key="i" class="link-item">
          <span class="link-item__label">{{ item.label }}</span>
          <a :href="item.url" class="link-item__url" target="_blank" rel="noopener">
            {{ item.url }}
          </a>
        </li>
        <li>
          <button class="card__edit-btn" @click="reset">Редактировать</button>
        </li>
      </ul>

      <!-- Edit mode -->
      <div v-else key="edit" class="edit-area">
        <textarea
          v-model="text"
          class="card__textarea"
          placeholder="В этом поле вы можете оставить как комментарии к занятию, так и ссылки на полезные материалы"
        />
        <button
          class="card__save-btn"
          :disabled="!links.length"
          @click="save"
        >
          Сохранить
        </button>
      </div>

    </Transition>
  </div>
</template>

<style scoped>
.card {
  background: #fff;
  border-radius: 16px;
  padding: 20px;
  width: 320px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
  font-family: 'Onest', sans-serif;
}

.card__title {
  font-size: 15px;
  font-weight: 600;
  color: #1a1a2e;
  margin: 0 0 12px;
}

.card__upload-btn {
  display: inline-block;
  padding: 5px 12px;
  background: #f0f0f2;
  border: 1px solid #d8d8de;
  border-radius: 8px;
  font-family: 'Onest', sans-serif;
  font-size: 13px;
  color: #1a1a2e;
  cursor: pointer;
  margin-bottom: 8px;
}

.card__upload-btn:hover {
  background: #e4e4ea;
}

.card__empty-files {
  font-size: 12px;
  color: #9898a8;
  margin: 0 0 14px;
}

/* Edit */
.edit-area {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.card__textarea {
  width: 100%;
  height: 110px;
  resize: none;
  border: 1px solid #e0e0e8;
  border-radius: 8px;
  padding: 10px 12px;
  font-family: 'Onest', sans-serif;
  font-size: 13px;
  color: #1a1a2e;
  outline: none;
  box-sizing: border-box;
  line-height: 1.5;
}

.card__textarea::placeholder {
  color: #b0b0bf;
}

.card__textarea:focus {
  border-color: #606fff;
}

.card__save-btn {
  align-self: flex-end;
  padding: 6px 16px;
  background: #606fff;
  border: none;
  border-radius: 8px;
  font-family: 'Onest', sans-serif;
  font-size: 13px;
  color: #fff;
  cursor: pointer;
  transition: background 0.15s, opacity 0.15s;
}

.card__save-btn:hover:not(:disabled) {
  background: #7b8fff;
}

.card__save-btn:disabled {
  opacity: 0.4;
  cursor: default;
}

/* Link list */
.link-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.link-item {
  display: flex;
  flex-direction: column;
  gap: 2px;
  min-width: 0;
}

.link-item__label {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.06em;
  color: #5a5a70;
  text-transform: uppercase;
}

.link-item__url {
  font-size: 13px;
  color: #606fff;
  text-decoration: none;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: block;
}

.link-item__url:hover {
  text-decoration: underline;
}

.card__edit-btn {
  margin-top: 4px;
  background: none;
  border: none;
  font-family: 'Onest', sans-serif;
  font-size: 12px;
  color: #9898a8;
  cursor: pointer;
  padding: 0;
  text-decoration: underline;
}

.card__edit-btn:hover {
  color: #606fff;
}

/* Transition */
.slide-enter-active,
.slide-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateY(8px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>
