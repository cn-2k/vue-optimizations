<template>
  <p class="loader">{{ text }}</p>
</template>

<script setup lang="ts">

withDefaults(defineProps<{
   text?: string
 }>(), {
     // here we have default values
     text: 'Carregando...'
 })
</script>
