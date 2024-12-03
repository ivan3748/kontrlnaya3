<template>
  <div class="comments">
    <h4>Комментарии</h4>
    <ul>
      <li v-for="(comment, index) in comments" :key="index">
        {{ comment }}
        <button @click="$emit('deleteComment', index)">Удалить</button>
      </li>
    </ul>
    <input v-model="newComment" placeholder="Добавить комментарий" />
    <button @click="addComment">Добавить</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  props: ['comments'],
  emits: ['addComment'],
  setup(_, { emit }) {
    const newComment = ref('');

    const addComment = () => {
      if (newComment.value) {
        emit('addComment', newComment.value);
        newComment.value = '';
      }
    };

    return { newComment, addComment };
  },
};
</script>
