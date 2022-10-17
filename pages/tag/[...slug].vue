<script setup lang="ts">
definePageMeta({ layout: "main" })
const route = useRoute()
const pathTo = route.params.slug.toString()
const { data } = await useAsyncData(() => {
  return queryContent()
    .sort({ date: -1 })
    .where({
      "tags": { $contains: pathTo },
    }) // exclude the Partial files
    .find()
})
</script>

<template>
  <div
    class="w-full max-w-screen-xl mx-auto px-4 py-4 grid grid-cols-1 gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4"
  >
    <NuxtLink
      :to="post._path"
      class="group p-4 bg-white shadow hover:shadow-lg dark:bg-slate-900 border border-slate-200 hover:border-slate-300 dark:border-slate-700 dark:hover:border-slate-500 rounded-xl transition duration-150"
      v-for="post in data"
      :key="post._id"
    >
      <div class="text-xs text-slate-400 dark:text-slate-500 mb-2">
        {{
          new Date(post.date).toLocaleDateString("ru", {
            // weekday: "long",
            year: "numeric",
            month: "long",
            day: "numeric",
          })
        }}
      </div>
      <h3
        class="leading-4 font-bold text-base text-slate-600 dark:text-slate-300 dark:group-hover:text-slate-100 transition duration-150"
      >
        {{ post.title }}
      </h3>
      <div
        v-if="post.tags"
        class="flex flex-wrap items-center justify-start mt-1"
      >
      
        <div
          v-for="tag in post.tags"
          :key="tag"
          class="px-2 py-0.5 mr-2 mt-2 leading-4 border border-slate-300 text-sm text-slate-500 group-hover:text-slate-600 dark:border-slate-600 dark:text-slate-500 dark:group-hover:text-slate-400 rounded-xl whitespace-nowrap transition duration-150 z-20"
        >
        {{ tag }}
        </div>
      </div>
    </NuxtLink>
  </div>
</template>
