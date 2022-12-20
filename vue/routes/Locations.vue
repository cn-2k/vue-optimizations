<template>
  <div class="container">
    <h1>Locations</h1>
    <WidgetLoader
      :url="mapComponent.url"
      :importFunction="mapComponent.importFunction"
    ></WidgetLoader>

    <!--Alternatively, load without SWRV-->
    <!-- <WidgetLoaderSimple
      :url="mapComponent.url"
      :importFunction="mapComponent.importFunction"
    ></WidgetLoaderSimple> -->
  </div>
</template>

<script setup>
import WidgetLoader from "../components/WidgetLoader";
import WidgetLoaderSimple from "../components/WidgetLoaderSimple";

    const mapComponent = {
      url: "https://api.npoint.io/ec46e59905dc0011b7f4",
      importFunction: () => import("../components/MapView.vue"),
    };
</script>
