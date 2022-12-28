<template>
  <div class="error">
    <svg viewBox="0 0 24 24" width="24" height="24">
      <path
        d="M13,13H11V7H13M13,17H11V15H13M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2Z"
      />
    </svg>
    <p>{{ errorMessage || "Unable to display component" }}</p>
  </div>
</template>

<script setup lang="ts">

const props = defineProps<{
  errorMessage?: string,
}>()
</script>
