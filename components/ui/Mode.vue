<script setup lang="ts">
import { SunIcon, MoonIcon } from "@heroicons/vue/20/solid"
type Theme = "light" | "dark"

const setColorTheme = (newTheme: Theme) => {
  useColorMode().preference = newTheme
}
</script>

<template>
  <button
    @click="setColorTheme($colorMode.preference === 'dark' ? 'light' : 'dark')"
    class="rounded-full focus:outline-none focus:ring-[1px] focus:ring-offset-2 focus:ring-slate-300 dark:focus:ring-slate-700"
  >
    <MoonIcon
      v-show="$colorMode.value === 'dark'"
      class="h-5 w-5 text-slate-400 hover:text-slate-200"
    />
    <SunIcon
      v-show="$colorMode.value === 'light'"
      class="h-5 w-5 text-slate-400 hover:text-slate-600"
    />
  </button>
</template>
