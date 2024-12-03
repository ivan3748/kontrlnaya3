<template>
  <div id="app">
    <h1>Дневник</h1>
    <PostForm @addPost="addPost" />
    <PostList 
      :posts="posts" 
      @deletePost="deletePost" 
      @editPost="editPost"
    />
  </div>
</template>

<script>
import { ref } from 'vue';
import PostForm from './components/PostForm.vue';
import PostList from './components/PostList.vue';

export default {
  components: { PostForm, PostList },
  setup() {
    const posts = ref([]);

    const addPost = (newPost) => {
      posts.value.push(newPost);
    };

    const deletePost = (id) => {
      posts.value = posts.value.filter(post => post.id !== id);
    };

    const editPost = (updatedPost) => {
      const index = posts.value.findIndex(post => post.id === updatedPost.id);
      if (index !== -1) {
        posts.value[index] = updatedPost;
      }
    };

    return { posts, addPost, deletePost, editPost };
  },
};
</script>
