<script setup>
const { query, params } = useRoute()
const slug = params.slug.join('/')
const language = query.lang

const storyblokApi = useStoryblokApi()
const story = ref(null)
const l10nOverride = ref(false)

try {
  const { data } = await storyblokApi.get('cdn/stories/localization/' + language + '/' + slug, { version: 'draft' })
  story.value = data.story
  l10nOverride.value = true
} catch {
  console.log('No l10n available for this language version of this story.')
  l10nOverride.value = false
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
  <LocalizationInfo v-if="l10nOverride" :full_slug="story.full_slug" />
  <StoryblokComponent v-if="story" :blok="story.content" />
</template>
