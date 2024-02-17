<template>
  <div class="hello mt-3">
    <ul class="list-unstyled">
      <li v-for="post in posts" :key="post.data.id" class="media m-3">
        <img class="mr-3" :src="post.data.thumbnail" :alt="post.data.title" />
        <div class="media-body">
          <h5 class="mt-0 mb-1">
            <a :href="createUrl(post.data.permalink)" target="_blank">{{ post.data.title }}</a>
          </h5>

          <h3 class="text-danger">{{ post.data.ups }} ⬆️</h3>
          <p>created {{ formatDate(post.data.created_utc) }} ago by {{ post.data.author }}</p>
          <span class="badge badge-pill badge-secondary"
            >{{ post.data.num_comments }} comments</span
          >
          <button
            v-if="isImage(post)"
            @click="post.showImage = !post.showImage"
            type="button"
            class="btn btn-primary"
          >
            {{ post.showImage ? 'Hide' : 'Show' }} Image
          </button>
          <div v-if="post.showImage">
            <img :src="post.data.url" alt="" />
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { onMounted } from 'vue'

const posts = ref([])

onMounted(() => {
  load()
})

const load = async () => {
  const response = await fetch('https://www.reddit.com/r/rarepuppers.json')
  const result = await response.json()
  console.log(result)
  posts.value = result.data.children
}

const createUrl = (permalink) => {
  return `https://www.reddit.com${permalink}`
}

const formatDate = (created_utc) => {
  const date = new Date(created_utc * 1000)
  return date.toLocaleString()
}

const isImage = (post) => {
  return (
    post.data.url.includes('jpg') ||
    post.data.url.includes('png') ||
    post.data.url.includes('jpeg') ||
    post.data.url.includes('bpm') ||
    post.data.url.includes('gif')
  )
}
</script>

<style scoped></style>
