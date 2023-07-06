<script setup>
const { params } = useRoute()
const slug = params.slug.join('/')

const story = await useAsyncStoryblok(`localization/${slug}`, {
  version: 'draft',
})
</script>

<template>
  <StoryblokComponent v-if="story" :blok="story.content" />
</template>
