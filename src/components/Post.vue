<script setup>
defineProps({
  post: Object
})
</script>

<template>
  <div class="post">
    <img :src="post.picture.large" />
    <h2>{{ post.name.first }} {{ post.name.last }}</h2>
    <a :href="`mailto:${post.email}`">{{ post.email }}</a>
  </div>
</template>

<style scoped>
.post {
  background: var(--second);
  max-width: 20rem;
  margin-left: auto;
  margin-right: auto;
  border-radius: 1rem;
  padding-bottom: 1rem;
}
.post:not(:first-child) {
  margin-top: 1rem;
}
.post h2 {
  font-size: 1.5rem;
  margin: 1rem 0 0;
  padding: 0 1rem;
}
.post a {
  color: var(--primary);
  padding: 0 1rem;
  display: block;
}
.post img{
  display: block;
  width: 100%;
  height: auto;
  border-radius: 1rem 1rem 0 0;
}
</style>