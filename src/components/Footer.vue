<template>
  <footer class="footer">
    <div class="openingHours">
      <p class="times">0:00-24:00</p>
      <p class="days">All Day.</p>
    </div>
    <ul class="navigation">
      <li v-for="content in navigationData"
      :key="content.id"
      :class="{ active: content.id === activeContent }"
      @click="changeNav(content)"
      class="item">
        {{ content.label }}
      </li>
    </ul>
  </footer>
</template>

<script setup>
  const props = defineProps({
    navigationData: Array,
    activeContent: Number
  })

  const emit = defineEmits(["change-nav"])

  const changeNav = (content) => {
    emit("change-nav", content)
  }
</script>

<style scoped>
  .footer {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-end;
  }

  .openingHours {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 0.5rem;
  }

  .navigation {
    display: flex;
    gap: 1rem;
  }

  .item {
    padding: 0.2rem 0.4rem;
    cursor: pointer;
  }

  .active {
    border-bottom: 1px solid #5f3819;
  }

  .times, .days {
    font-size: 1.3rem;
  }

  @media screen and (max-width: 964px) {
    .openingHours {
      display: none;
    }

    .navigation {
      position: fixed;
      left: 0;
      bottom: 0;
      justify-content: space-between;
      width: 100%;
      background-color: #fff;
      padding: 1rem 3rem 3rem;
    }
  }

  @media screen and (min-width: 965px) {
    .navigation {
      flex-direction: column;
    }
  }
</style>