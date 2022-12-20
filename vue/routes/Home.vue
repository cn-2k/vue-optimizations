<template>
  <div class="container">
    <h1>Home</h1>
    <div class="grid">
      <!-- <WidgetLoader
        v-for="component in components"
        :key="component.url"
        v-bind="component"
      ></WidgetLoader> -->

      <!--Alternatively, load without SWRV-->
      <WidgetLoaderSimple
        v-for="component in components"
        :key="component.url"
        v-bind="component"
      ></WidgetLoaderSimple>
    </div>
  </div>
</template>

<script setup>
import WidgetLoader from "../components/WidgetLoader";
import WidgetLoaderSimple from "../components/WidgetLoaderSimple";

    const components = [
      {
        url: "https://api.npoint.io/01264aa2a713715ccc1e",
        importFunction: () => import("../components/KPI.vue"),
      },
      {
        url: "https://api.npoint.io/ea45973ff614bdbc7ed1",
        importFunction: () => import("../components/KPI.vue"),
      },
      {
        url: "https://api.npoint.io/8d900f8ba26cba4acce7",
        importFunction: () => import("../components/KPI.vue"),
      },
      {
        url: "https://api.npoint.io/04459c847fdd2a1d84e3",
        importFunction: () => import("../components/DataTable.vue"),
      },
    ];
</script>
