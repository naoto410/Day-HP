<template>
  <div class="layout">
    <Header :content="activeContent" />
    <Main />
    <Footer :navigationData="navigationData" :activeContent="activeContent.id" @change-nav="changeSection" />
  </div>
</template>

<script setup>
  import { ref } from "vue"
  import Header from './components/Header.vue';
  import Main from './components/Main.vue';
  import Footer from './components/Footer.vue';
  import { navigationData } from './data/navigationData';

  const activeContent = ref(navigationData[0])
  console.log(navigationData)

  const changeSection = (content) => {
    activeContent.value = content
  }
</script>

<style scoped>
  .layout {
    display: flex;
    padding: 4.5rem;
  }

  .layout > * {
    flex: 1;
  }
</style>
