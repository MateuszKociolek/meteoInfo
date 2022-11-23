<template>
  <div class="container-fluid">
    <div class="text-center">
      <h2>Meteo info</h2>
    </div>
    <meteo></meteo>
  </div>
</template>

<script>
  import meteo from './components/meteo.vue';
  
  export default {
    components: {
      meteo,
    },
  };
  
</script>

<style>
</style>
