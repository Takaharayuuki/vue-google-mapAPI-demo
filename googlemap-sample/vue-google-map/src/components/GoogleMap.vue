<template>
  <div>
    <h1>Google Map</h1>
    <input type="text" v-model="address" >
    <button type="button" @click="mapSearch">検索</button>
    <div id="map"></div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      map: {},
      marker: null,
      geocoder: {},
      address:'',
      myLatLng:{},
      lat:'',
      lng:''
    }
  },
  mounted(){
    if(!window.mapLoadStarted){
      window.mapLoadStarted = true;
      let script = document.createElement('script');
      script.src = process.env.VUE_APP_API_MAP;
      script.async = true;
      document.head.appendChild(script);
    }

    window.initMap = () => {
      window.mapLoaded = true;
      this.map = new window.google.maps.Map(document.getElementById('map'))
      this.geocoder = new window.google.maps.Geocoder();
    }
  },
  methods: {
    mapSearch(){
      this.geocoder.geocode({
        'address': this.address
      }, (results, status) => {
          if(status === window.google.maps.GeocoderStatus.OK) {
            this.map.setCenter(results[0].geometry.location);
            this.lat = results[0].geometry.location.lat();
            this.lng = results[0].geometry.location.lng();
            console.log(this.lat);
            console.log(this.lng);
            this.myLatLng.lat = this.lat;
            this.myLatLng.lng = this.lng;
            console.log(this.myLatLng);
            this.map = new window.google.maps.Map(this.$refs.map, {
              center: this.myLatLng,
              zoom: 8
            });
            new window.google.maps.Marker({position:this.myLatLng,map:this.map})
        }
      });
    }
  },
};
</script>