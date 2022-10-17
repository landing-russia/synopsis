<script setup lang="ts">
definePageMeta({ layout: "main" })
const route = useRoute()
const pathTo = route.params.slug.toString()
const { data } = await useAsyncData(() => {
  return queryContent(pathTo)
    .sort({ date: -1 }) // show latest articles first
    .where({ _partial: false, _path: { $ne: "/" } }) // exclude the Partial files
    .find()
})
</script>

<template>
  <p>{{ $route.params.slug }}</p>
  <p>{{ pathTo }}</p>
</template>
