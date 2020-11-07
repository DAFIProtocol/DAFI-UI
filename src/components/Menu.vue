<template>
    <div id="footer" class="d-flex justify-content-center">
        <span class="col-4 ic"><router-link :to="`/`" style="color: #eee"><i class="fas fa-circle-notch" style='font-size:36px'></i></router-link></span><router-link :to="`/about`" class="circ"><i class='fas fa-exchange-alt' style='font-size:36px'></i>
    </router-link>
         <span class="col-4 ic"><router-link :to="`/info`" style="color: #eee"><i class="material-icons" style='font-size:36px; margin-top: 5px'>menu</i></router-link></span>
    </div>
</template>

<script>
  export default {
    name: 'Menu'
  }
</script>

<style scoped>

</style>
