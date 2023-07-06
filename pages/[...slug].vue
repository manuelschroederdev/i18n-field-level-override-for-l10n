<script setup>
const { query, params } = useRoute()
const slug = params.slug.join('/')
const language = query.lang

const storyblokApi = useStoryblokApi()
const story = ref(null)

console.log('cdn/stories/localization/' + language + '/' + slug)

//stories/localization/de/an-example-landing-page

try {
  const { data } = await storyblokApi.get(
    'cdn/stories/localization/' + language + '/' + slug,
    { version: 'draft' }
  )
  story.value = data.story
} catch {
  console.log('No l10n available for this language version of this story.')
  const { data } = await storyblokApi.get('cdn/stories/' + slug, {
    version: 'draft',
    language,
  })
  story.value = data.story
}

onMounted(() => {
  useStoryblokBridge(story.value.id, (evStory) => (story.value = evStory))
})
</script>

<template>
  <StoryblokComponent v-if="story" :blok="story.content" />
</template>
