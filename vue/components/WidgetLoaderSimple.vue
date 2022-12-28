<template>
  <div class="widget" :style="{ 'aspect-ratio': loading ? aspectRatio : '' }">
    <Transition>
      <component :is="AsyncComponent" v-bind="componentProps"></component>
    </Transition>
  </div>
</template>

<script setup lang="ts">
import {
  ref,
  defineAsyncComponent,
  computed,
  onBeforeUnmount,
} from "vue";
import Loader from "./Loader.vue";
import Error from "./Error.vue";

const props = withDefaults(defineProps<{
  aspectRatio?: string,
  url: string,
  importFunction: () => any,
}>(), {
  aspectRatio: "5 / 3"
})

const data = ref(null);
const loading = ref(true);
const controller = new AbortController();

const loadComponent = () => {
  return fetch(props.url, { signal: controller.signal })
    .then((response) => response.json())
    .then((response) => (data.value = response))
    .then(props.importFunction)
    .catch((e) => console.error(e))
    .finally(() => (loading.value = false));
};

const componentProps = computed(() => {
  return {
    data: data.value,
    color: "turquoise",
  };
});

const AsyncComponent = defineAsyncComponent({
  loader: loadComponent,
  loadingComponent: Loader,
  errorComponent: Error,
  // delay: 200,
  timeout: 5000,
});

onBeforeUnmount(() => controller.abort());
</script>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
