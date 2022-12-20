<template>
  <div>
    <p>{{ data }}</p>
    <div class="widget" :style="{ 'aspect-ratio': loading ? aspectRatio : '' }">
      <slot :data="data" v-if="data"></slot>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  data: Array,
})

  const data = props.data;
</script>
