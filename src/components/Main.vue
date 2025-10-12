<template>
  <main class="main">
    <div class="mainVisual">
      <Transition name="fade">
        <img :src="currentImage" :key="currentImage" alt="画像" class="mainImg">
      </Transition>
    </div>
    <div class="labels">
      <button
      v-for="(image, i) in images"
      :key="image"
      class="imgLabel"
      :class="{ active: currentImage === image }"
      @click="selectImage(image)"
      :aria-label="`画像 ${i + 1}`">
    </button>
    </div>
  </main>
</template>

<script setup>
  import { ref, onMounted, onUnmounted } from "vue"

  const modules = import.meta.glob('../assets/images/*.{jpg,jpeg,png}', { eager: true, query: '?url', import: 'default' })
  const images = Object.keys(modules).sort().map(k => modules[k])
  const currentImage = ref(images[0] ?? '')

  let currentIndex = 0
  let timerId = null

  const startTimer = () => {
    if (timerId) clearInterval(timerId)
    timerId = setInterval(() => {
      currentIndex = (currentIndex + 1) % images.length
      currentImage.value = images[currentIndex]
    }, 3000)
  }

  const selectImage = (newImg) => {
    currentImage.value = newImg
    currentIndex = images.indexOf(newImg)
    startTimer()
  }

  onMounted(() => {
    startTimer()
  })

  onUnmounted(() => {
    if(timerId) clearInterval(timerId)
  })
</script>

<style scoped>
  .main {
    position: relative;
    display: flex;
    justify-content: center;
  }

  .mainVisual {
    aspect-ratio: 1 / 1.7;
    position: relative;
    border-radius: 50% 50% 0 0 / 30% 30% 0 0 ;
    overflow: hidden;
  }

  .mainImg {
    position: absolute;
    top: 0;
    left: 0;
    display: block;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .labels {
    position: absolute;
    display: flex;
    gap: 1rem;
  }

  .imgLabel {
    width: 0.7rem;
    height: 0.7rem;
    background-color: rgba(95, 56, 25, 0.3);
    border: none;
    cursor: pointer;
  }

  .active {
    background-color: #5f3819;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: transform 0.5s;
    will-change: transform;
  }

  .fade-enter-from {
    transform: translateX(100%);
  }

  .fade-enter-to {
    transform: translateX(0);
  }

  .fade-leave-from {
    transform: translateX(0);
  }

  .fade-leave-to {
    transform: translateX(-100%);
  }

  @media screen and (max-width: 964px) {
    .main {
      max-width: calc(100vh - 6rem);
      width: 100%;
      margin-bottom: 4rem;
    }

    .mainVisual {
      width: 100%;
    }

    .labels {
      bottom: -2rem;
      left: 50%;
      transform: translateX(-50%);
    }
  }

  @media screen and (min-width: 965px) {
    .mainVisual {
      height: calc(100vh - 9rem);
      width: 413px;
      height: 700px;
      width: min(90%, calc(var(--max-h) / 1.7));
      max-width: calc(var(--max-h) / 1.7);
      max-height: var(--max-h);
    }

    .labels {
      bottom: 0;
      right: -2rem;
      flex-direction: column;
    }
  }
</style>