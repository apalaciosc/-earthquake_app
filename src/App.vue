<template>
  <ion-app>
    <ion-content>
      <DrawMap class="map" />
    </ion-content>
  </ion-app>
</template>

<script>
import DrawMap from "./components/DrawMap";

export default {
  name: "App",
  components: {
    DrawMap
  }
};
</script>

<style lang="scss" scoped>
.map {
  height: 425px;
}
</style>
