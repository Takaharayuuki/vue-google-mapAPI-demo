<template>
  <div>
    <h1>Google Map</h1>
    <div ref="map" style="height: 500px; width:800px;"></div>
  </div>
</template>

<script>
export default {
  props: {
    myLatLng: {
      type: Object,
      required:true,
     },
     zoom: {
       type:Number,
       required: true
     }
  },
  data(){
    return {
      map: '',
    }
  },
  mounted(){
    console.log(this.key);
    let script = document.createElement('script');
    script.src = process.env.VUE_APP_API_MAP;
    script.async = true;
    document.head.appendChild(script);

    window.initMap = () => {
      this.map = new window.google.maps.Map(this.$refs.map,{
        center: this.myLatLng,
        zoom: this.zoom
      });
      new window.google.maps.Marker({position:this.myLatLng,map:this.map})
    }
  }
}
</script>