<template>
  <div>
    <LoadingSpinner v-if="loading" />
    <div v-else>
      <h1 class="text-3xl font-bold mb-4">{{ post.title }}</h1>
      <p>{{ post.content }}</p>
      <NuxtLink to="/" class="text-blue-500 mt-6 inline-block">Back to Home</NuxtLink>
    </div>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
import { ref, onMounted } from 'vue';
import LoadingSpinner from '@/components/LoadingSpinner.vue';
import postsData from "../static/data/posts.json";

const route = useRoute();
const post = ref(null);
const loading = ref(true);

const fetchPost = () => {  
  post.value = postsData.find((p) => p.slug === route.params.slug);
  loading.value = false;
};

onMounted(() => {
  fetchPost();
});
</script>
