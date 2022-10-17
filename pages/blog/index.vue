<script setup lang="ts">
definePageMeta({ layout: "main" })
const { data } = await useAsyncData(() => {
  return queryContent("/blog/")
    .sort({ date: -1 }) // show latest articles first
    .where({ _partial: false, _path: { $ne: "/blog" } }) // exclude the Partial files
    .find()
})
</script>

<template>
  <div class="prose dark:prose-invert lg:prose-lg w-full max-w-prose md:max-w-2xl lg:max-w-3xl mx-auto my-12 px-4 space-y-8">
    <div v-for="post in data" :key="post._id">
      <div class="text-xs text-slate-500">
        {{
          new Date(post.date).toLocaleDateString("ru", {
            // weekday: "long",
            year: "numeric",
            month: "long",
            day: "numeric",
          })
        }}
      </div>
      <NuxtLink :to="post._path" class="leading-3">{{ post.title }}</NuxtLink>
      <div class="mt-2 text-sm text-slate-400">{{ post.description }}</div>
    </div>
  </div>
</template>
