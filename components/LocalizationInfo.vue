<script setup>
defineProps({ full_slug: String })
</script>
<template>
  <header
    class="rounded-md shadow-lg container max-w-xl py-3 px-6 top-3 left-1/2 -translate-x-1/2 fixed border-[#50b0ae] bg-white backdrop-blur-lg border bg-opacity-50 text-sm"
  >
    You're viewing the story located in
    <span class="text-[#50b0ae] font-bold">{{ full_slug }}</span
    >. Navigate to this story to edit the content or remove it in order to use the default field level translation.
  </header>
</template>
