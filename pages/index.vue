<template>
  <div>
    <h1 class="text-3xl font-bold mb-6">Blog Posts</h1>
    <input
      v-model="query"
      type="text"
      placeholder="Search posts..."
      class="border rounded p-2 mb-6 w-full"
    />

    <LoadingSpinner v-if="loading" />

    <div v-if="error" class="text-red-500 mb-4">
      <p>Error loading posts. Please try again later.</p>
    </div>

    <div v-else>
      <div v-if="filteredPosts.length === 0" class="text-gray-500 text-center">
        <p>No posts found matching your search.</p>
      </div>

      <div v-else class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <PostCard v-for="post in filteredPosts" :key="post.slug" :post="post" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import PostCard from "../components/PostCard.vue";
import LoadingSpinner from "../components/LoadingSpinner.vue";
import postsData from "../static/data/posts.json";

const posts = ref(postsData);
const query = ref("");
const loading = ref(false);
const error = ref(false);

const filteredPosts = computed(() =>
  (posts.value || []).filter((post) =>
    post.title.toLowerCase().includes(query.value.toLowerCase())
  )
);

onMounted(() => {
  loading.value = false;
});
</script>
