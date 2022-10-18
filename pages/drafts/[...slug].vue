<template>
  <main>
    <ContentDoc v-slot="{ doc }">
      <div class="text-sm text-slate-500 mb-6">
        {{
          new Date(doc.date).toLocaleDateString("ru", {
            // weekday: "long",
            year: "numeric",
            month: "long",
            day: "numeric",
          })
        }}
      </div>
      <h1 class="leading-tight">
        {{ doc.title }}
      </h1>
      <ContentRenderer :value="doc" />
      <div v-if="doc.tags" class="flex flex-wrap items-center justify-start mt-1">
        <a
          :href="`/tag/${tag}`"
          v-for="tag in doc.tags"
          :key="tag"
          class="px-2 py-1 mr-2 mt-2 leading-4 border border-slate-300 text-base text-slate-500 group-hover:text-slate-600 dark:border-slate-600 dark:text-slate-500 dark:group-hover:text-slate-400 rounded-xl whitespace-nowrap transition duration-150"
        >
          {{ tag }}
        </a>
      </div>
    </ContentDoc>
  </main>
</template>
