<template>
  <div>
    <h1>Google Map</h1>
  </div>
</template>

<script>
export default {
  mounted(){
    console.log(window.google)
    setTimeout(() => {
      if(!window.google){
        console.log('ロードに時間がかかっています。');
      } else {
        console.log(window.google);
      }
    },3000)
  }
}
</script>