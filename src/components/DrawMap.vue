<template>
  <LoadMap
    :configMap="configMap"
    apiKey="AIzaSyAPcxYRnRn_5FIMMTthBORWpWiRcgMUjnM"
  >
    <template slot-scope="{ google, map }">
      <Markers
        v-for="marker in markers"
        :key="marker.id"
        :marker="marker"
        :google="google"
        :map="map"
      />
    </template>
  </LoadMap>
</template>

<script>

  import LoadMap from "./LoadMap";
  import Markers from "./Markers";
  import { configMap } from "@/constants/configMap";
  import axios from "axios";

  export default {
    components: {
      LoadMap,
      Markers
    },

    data() {
      return {
        markers: [],
        default_marker: [
            {
              state: 1,
              utc_time: "2020/06/04 21:53:55",
              chilean_time: "2020/06/04 17:53:55",
              reference: "145 km al N de Sofifi - Indonesia",
              magnitude: 4.4,
              scale: "Mb",
              latitude: 2.0503,
              longitude: 127.5452,
              depth: 76.85,
              id: "56893999",
              url: "http://sismologia.net/?p=detalles&id=56893999",
              source: "INSIMU"
          },
        ]
      };
    },

    async mounted(){
      const response = await axios.get('https://chilealerta.com/api/query/?user=demo&select=ultimos_sismos')
      let last_eartquakes = response.data.ultimos_sismos
      if (last_eartquakes) {
        this.markers = last_eartquakes
      } else {
        this.markers = this.default_marker
      }
    },

    computed: {
      configMap() {
        return {
          ...configMap,
          center: this.mapCenter
        };
      },

      mapCenter() {
        return { lat: 2.0503, lng: 127.5452 };
      }
    }
  };

</script>