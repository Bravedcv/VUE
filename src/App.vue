<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import axios from "axios";
import { ref, onMounted } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
const getX = async () => {
  try {
        const response = await axios.get(`https://jsonplaceholder.typicode.com/posts`);
        console.log(response.data);
        return response.data;
    } catch (err) {
        console.error(err);
        return [];
    }
}
const posts = ref([])

onMounted(async () => {
  const lstPosts = await getX();
  posts.value = lstPosts;
})
    
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
    <HelloWorld msg="Vite + Vue" />
    <p v-for="post in posts" :key="post.id">{{post.title}}</p>
  </div>
  
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
