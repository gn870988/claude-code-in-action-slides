<script setup>
import { ref, computed, nextTick, onBeforeUnmount } from 'vue'

const props = defineProps({
  src: { type: String, default: '' },
  youtube: { type: String, default: '' },
})

const useYoutube = ref(false)
const isExpanded = ref(false)
const isPlaying = ref(false)
const videoRef = ref(null)
const expandedVideoRef = ref(null)
const lastTimestamp = ref(0)

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

const syncPlayingState = () => {
  const video = isExpanded.value ? expandedVideoRef.value : videoRef.value
  isPlaying.value = !!video && !video.paused && !video.ended
}

const togglePlayback = async () => {
  const video = isExpanded.value ? expandedVideoRef.value : videoRef.value
  if (!video) return

  if (video.paused || video.ended) {
    await video.play()
  }
  else {
    video.pause()
  }

  syncPlayingState()
}

const handleKeydown = (event) => {
  if (!isExpanded.value) return

  if (event.code === 'Space') {
    event.preventDefault()
    event.stopImmediatePropagation()
    togglePlayback()
  }

  if (event.key === 'Escape') {
    event.preventDefault()
    event.stopImmediatePropagation()
    closeExpanded()
  }
}

const openExpanded = async () => {
  const video = videoRef.value
  lastTimestamp.value = video?.currentTime ?? 0
  const shouldPlay = !!video && !video.paused && !video.ended

  video?.pause()
  isExpanded.value = true
  await nextTick()
  window.addEventListener('keydown', handleKeydown, { capture: true })

  const expandedVideo = expandedVideoRef.value
  if (!expandedVideo) return

  expandedVideo.currentTime = lastTimestamp.value
  expandedVideo.focus()
  if (shouldPlay) {
    await expandedVideo.play()
  }
  syncPlayingState()
}

const closeExpanded = () => {
  const expandedVideo = expandedVideoRef.value
  lastTimestamp.value = expandedVideo?.currentTime ?? lastTimestamp.value
  expandedVideo?.pause()
  isExpanded.value = false
  window.removeEventListener('keydown', handleKeydown, { capture: true })

  nextTick(() => {
    if (videoRef.value) {
      videoRef.value.currentTime = lastTimestamp.value
    }
    syncPlayingState()
  })
}

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, { capture: true })
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
  <div
    v-else
    class="demo-video-shell"
  >
    <video
      ref="videoRef"
      :src="src"
      controls
      class="demo-video"
      tabindex="0"
      @error="handleError"
      @play="syncPlayingState"
      @pause="syncPlayingState"
      @ended="syncPlayingState"
    />
    <button
      type="button"
      class="demo-video-expand"
      :aria-label="isExpanded ? '離開影片最大化' : '影片最大化'"
      @click="isExpanded ? closeExpanded() : openExpanded()"
    >
      {{ isExpanded ? '還原' : '最大化' }}
    </button>

    <Teleport to="body">
      <div
        v-if="isExpanded"
        class="demo-video-overlay"
      >
        <video
          ref="expandedVideoRef"
          :src="src"
          class="demo-video-overlay-player"
          tabindex="0"
          @click="togglePlayback"
          @play="syncPlayingState"
          @pause="syncPlayingState"
          @ended="syncPlayingState"
        />
        <button
          type="button"
          class="demo-video-overlay-close"
          aria-label="離開影片最大化"
          @click="closeExpanded"
        >
          還原
        </button>
      </div>
    </Teleport>
  </div>
</template>
