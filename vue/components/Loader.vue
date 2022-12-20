<template>
  <p class="loader">{{ text }}</p>
</template>

<script setup>

  const props = defineProps({
  text: String,
  default: "Loading...",
})
    const { text } = props;
</script>
