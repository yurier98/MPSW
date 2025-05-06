<template>
  <div>
    <NuxtLink v-if="logo.light && logo.dark" class="flex">
      <NuxtImg :src="logo.light" class="h-11 dark:hidden" />
      <span v-if="showTitle && title" class="ml-3 self-center font-bold">
        {{ title }}
      </span>
    </NuxtLink>
  </div>
</template>

<script setup lang="ts">
const { logo, title, showTitle } = useConfig().value.header;
</script>
