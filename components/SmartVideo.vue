<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  src: { type: String, default: '' },
  youtube: { type: String, default: '' },
})

const useYoutube = ref(false)

const handleError = () => {
  if (props.youtube) useYoutube.value = true
}

const youtubeEmbedUrl = computed(() => {
  if (!props.youtube) return ''
  const match = props.youtube.match(
    /(?:youtu\.be\/|youtube\.com\/(?:watch\?v=|embed\/|shorts\/))([^&?\s]+)/
  )
  const id = match ? match[1] : props.youtube
  return `https://www.youtube.com/embed/${id}?rel=0`
})
</script>

<template>
  <iframe
    v-if="useYoutube"
    :src="youtubeEmbedUrl"
    class="demo-video demo-video-iframe"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
  />
  <video
    v-else
    :src="src"
    controls
    class="demo-video"
    @error="handleError"
  />
</template>
