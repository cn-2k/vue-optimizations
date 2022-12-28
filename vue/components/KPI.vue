<template>
  <div class="kpi" v-if="data">
    <h2 class="kpi__title">
      <span class="kpi__name">{{ data.title }}</span>
      <span class="kpi__value"
        >{{ data.value }}<span class="kpi__unit">{{ data.unit }}</span></span
      >
    </h2>
    <figure>
      <LineGraph :data="data.data" :color="color"></LineGraph>
    </figure>
  </div>
</template>

<script setup lang="ts">
import LineGraph from "./LineGraph.vue";

interface DataProps{
  title: string,
  unit: string,
  value: string,
  data: any,
}

defineProps<{
  data: DataProps,
  color: string
}>();
</script>
