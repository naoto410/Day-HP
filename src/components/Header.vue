<template>
  <header class="header">
    <h1 class="logo">
      <img src="../assets/day.svg" alt="" class="img">
    </h1>
    <p class="mainContents">
      {{ content.description }}
    </p>
  </header>
</template>

<script setup>
  const props = defineProps({
    content: Object
  })
</script>

<style scoped>
  .header {
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }

  .logo {
    width: 15rem;
  }

  .img {
    width: 100%;
  }

  .mainContents {
    font-size: 0.8rem;
    line-height: 1.5rem;
    white-space: pre-line;
  }

  @media screen and (min-width: 965px) {
    .header {
      padding-right: 2rem;
      gap: 4.5rem;
    }
  }
</style>