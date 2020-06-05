<script>

  export default {
    props: {
      google: {
        type: Object,
        required: true
      },
      map: {
        type: Object,
        required: true
      },
      marker: {
        type: Object,
        required: true
      }
    },

    mounted() {
      const { Marker } = this.google.maps;

      const markerColor = function(marker) {
        let magnitude = marker.magnitude
        if (magnitude > 0 && magnitude < 4) {
          return 'green'
        }
        else if (magnitude >= 4 && magnitude < 6){
          return 'yellow'
        }
        else {
          return 'red'
        }
      }

      new Marker({
        position: { lat: this.marker.latitude, lng: this.marker.longitude },
        marker: this.marker,
        map: this.map,
        title: this.marker.title,
        icon: {
            path: this.google.maps.SymbolPath.FORWARD_CLOSED_ARROW,
            strokeColor: markerColor(this.marker),
            scale: 3
        }
      });

    },

    render() {}
  };

</script>