<template>
  <div
    class="widget"
    :style="{ 'aspect-ratio': shouldShowLoader ? aspectRatio : '' }"
  >
    <Loader v-if="shouldShowLoader"></Loader>
    <Error v-else-if="error" :errorMessage="error.message"></Error>
    <Transition>
      <component
        :is="AsyncComponent"
        v-bind="componentProps"
        v-if="data"
      ></component>
    </Transition>

    <!--Small spinner to be shown while component is revalidating-->
    <Loader
      v-if="isValidating && data"
      class="widget__validating"
      text=""
      aria-hidden="true"
    ></Loader>
  </div>
</template>

<script setup>
import { defineAsyncComponent, computed } from "vue";
import Loader from "./Loader";
import Error from "./Error";
import { useLazyFetch } from "../composables/lazyFetch";

  const props = defineProps({
    aspectRatio: {
         type: String,
         default: "5 / 3"
     },
     url: String,
     importFunction: Function,
})

    const { aspectRatio, url, importFunction } = props;

    const componentProps = computed(() => {
      return {
        data: data.value,
        color: "turquoise",
      };
    });

    const { data, isValidating, error } = useLazyFetch(url);

    const shouldShowLoader = computed(() => isValidating.value && !data.value);

    const AsyncComponent = defineAsyncComponent({
      loader: importFunction,
      delay: 200,
      timeout: 5000,
    });
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
