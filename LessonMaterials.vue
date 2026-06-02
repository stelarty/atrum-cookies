<script setup>
import { ref } from 'vue'

const links = ref([
  {
    label: 'ЭТА ССЫЛКА ВЕДЁТ НА ФИГМУ',
    url: 'https://www.figma.com/design/fX8yBmgChzurXmCENygGQu/Преподаватели?node-id=3217-19269&t=5Fr1LLayFpUKSYIs-1'
  },
  {
    label: 'МАКЕТЫ ФИГМЫ',
    url: 'https://www.figma.com/design/fX8yBmgChzurXmCENygGQu/Преподаватели?node-id=3217-19269&t=5Fr1LLayFpUKSYIs-1'
  },
  {
    label: 'ОПИСАНИЕ ССЫЛКИ',
    url: 'https://www.figma.com/design/fX8yBmgChzurXmCENygGQu/Преподаватели?node-id=3217-19269&t=5Fr1LLayFpUKSYIs-1'
  }
])
</script>

<template>
  <div class="card">
    <h2 class="card__title">Материалы урока</h2>

    <button class="card__upload-btn">Добавить файл</button>
    <p class="card__empty-files">Материалов пока нет</p>

    <ul v-if="links.length" class="link-list">
      <li v-for="(item, i) in links" :key="i" class="link-item">
        <span class="link-item__label">{{ item.label }}</span>
        <a :href="item.url" class="link-item__url" target="_blank" rel="noopener">{{ item.url }}</a>
      </li>
    </ul>

    <textarea
      v-else
      class="card__textarea"
      placeholder="В этом поле вы можете оставить как комментарии к занятию, так и ссылки на полезные материалы"
    />
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
  font-weight: 400;
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

/* Empty textarea */
.card__textarea {
  width: 100%;
  height: 100px;
  resize: none;
  border: 1px solid #e0e0e8;
  border-radius: 8px;
  padding: 10px 12px;
  font-family: 'Onest', sans-serif;
  font-size: 13px;
  color: #1a1a2e;
  outline: none;
  box-sizing: border-box;
}

.card__textarea::placeholder {
  color: #b0b0bf;
}

.card__textarea:focus {
  border-color: #606fff;
}
</style>
