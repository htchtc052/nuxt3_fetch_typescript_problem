<script setup lang="ts">

interface Post {
  id: number;
  userId: number;
  title: string;
}

const { data: posts, pending } = await useAsyncData<Post[]>(
"posts",
() => $fetch("https://jsonplaceholder.typicode.com/posts"),
{
default: (): Post[] => [],
}
);

console.debug(posts.value);
</script>
<template>

  <div v-if="pending">Loading...</div>
  <div v-else>
    <ul>
      <li v-for="post of posts" :key="post.id">{{ post.title }}</li>
    </ul>

  </div>
</template>

<style scoped></style>
