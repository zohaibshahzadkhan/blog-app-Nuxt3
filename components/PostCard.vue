<template>
  <div class="border p-4 rounded shadow hover:shadow-lg">
    <h2 class="text-xl font-semibold">{{ post.title }}</h2>
    <p>{{ post.excerpt }}</p>
    <NuxtLink :to="`/posts/${post.slug}`" class="text-blue-500 mt-2 block">
      Read More
    </NuxtLink>
  </div>
</template>

<script setup>
defineProps({
  post: {
    type: Object,
    required: true,
  },
});
</script>
