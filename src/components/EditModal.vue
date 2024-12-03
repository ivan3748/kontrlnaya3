<template>
  <div class="modal">
    <div class="modal-content">
      <h3>Редактирование поста</h3>
      <textarea v-model="editedContent"></textarea>
      <button @click="save">Сохранить</button>
      <button @click="$emit('close')">Закрыть</button>
    </div>
  </div>
</template>

<script>
import { ref, watch } from 'vue';

export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  emits: ['close', 'save'],
  setup(props, { emit }) {
    const editedContent = ref(props.post.content);

    watch(
      () => props.post.content,
      (newContent) => {
        editedContent.value = newContent;
      }
    );

    const save = () => {
      emit('save', { ...props.post, content: editedContent.value });
    };

    return { editedContent, save };
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #3f0055;
  padding: 20px;
  border-radius: 8px;
  width: 90%;
  max-width: 400px;
  color: #e0d4f7;
}

.modal-content textarea {
  width: 100%;
  background-color: #4d1568;
  border: 1px solid #6e2a96;
  color: #fff;
  padding: 10px;
  border-radius: 5px;
}

.modal-content button {
  margin-top: 10px;
}
</style>
