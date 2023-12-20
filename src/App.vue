<script setup>
import Post from './components/Post.vue'
import { ref, onMounted, onUnmounted } from 'vue'

let posts = ref([]),
    scrollComponent = ref(null),
    checkpoint = true

const getPosts = async () => {
  try {
    const response = await fetch(`https://randomuser.me/api/?results=10`);
    const data = await response.json();
    posts.value.push(...data.results)
    console.log(posts.value.length)
    checkpoint = true
  } catch (error) {
    alert('Something went wrong! Please check console logs.')
    console.dir(error)
  }
}
getPosts()

const handleScroll = () => {
  let element = scrollComponent.value
  if (element.getBoundingClientRect().bottom - 100 < window.innerHeight && checkpoint) {
    getPosts()
    checkpoint = false
  }
}

onMounted(() => {
  window.addEventListener("scroll", handleScroll)
})

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll)
})
</script>

<template>
  <div class="post-list" ref="scrollComponent">
    <Post v-for="post in posts" :post="post" />
  </div>
</template>

<style scoped>
.post-list{
  padding: 2rem 0;
}
</style>