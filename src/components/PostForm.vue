<template>
  <div class="post-form">
    <input v-model="title" placeholder="Введите заголовок" />
    <textarea v-model="content" placeholder="Введите текст поста"></textarea>
    <button @click="handleAddPost">Добавить пост</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ['addPost'],
  setup(_, { emit }) {
    const title = ref('');
    const content = ref('');

    const handleAddPost = () => {
      if (title.value && content.value) {
        emit('addPost', { id: Date.now(), title: title.value, content: content.value, comments: [] });
        title.value = '';
        content.value = '';
      }
    };

    return { title, content, handleAddPost };
  },
};
</script>
