<template>
  <div class="post-list">
    <div v-for="post in posts" :key="post.id" class="post-item">
      <h3>{{ post.title }}</h3>
      <p>{{ post.content }}</p>
      <button @click="deletePost(post.id)">Удалить</button>
      <button @click="openEditModal(post)">Изменить</button>
      <button @click="toggleComments(post.id)">
        {{ post.isCommentsVisible ? 'Скрыть комментарии' : 'Показать комментарии' }}
      </button>
      <CommentList v-if="post.isCommentsVisible" :comments="post.comments" @addComment="addComment(post.id)" />
    </div>
    <EditModal v-if="modalVisible" :post="editablePost" @close="closeModal" @save="saveChanges" />
  </div>
</template>

<script>
import { ref } from 'vue';
import CommentList from './CommentList.vue';
import EditModal from './EditModal.vue';

export default {
  components: { CommentList, EditModal },
  props: ['posts'],
  emits: ['deletePost', 'editPost'],
  setup(props, { emit }) {
    const modalVisible = ref(false);
    const editablePost = ref(null);

    const deletePost = (id) => {
      emit('deletePost', id);
    };

    const openEditModal = (post) => {
      modalVisible.value = true;
      editablePost.value = { ...post };
    };

    const closeModal = () => {
      modalVisible.value = false;
    };

    const saveChanges = (post) => {
      emit('editPost', post);
      closeModal();
    };

    const toggleComments = (id) => {
      const post = props.posts.find(post => post.id === id);
      if (post) {
        post.isCommentsVisible = !post.isCommentsVisible;
      }
    };

    const addComment = (id, comment) => {
      const post = props.posts.find(post => post.id === id);
      if (post) {
        post.comments.push(comment);
      }
    };

    return { modalVisible, editablePost, deletePost, openEditModal, closeModal, saveChanges, toggleComments, addComment };
  },
};
</script>
