<template>
<div class="home"> 
 <contenido />
</div>
 
</template>

<script>
  import contenido from '../components/contenidoComponent'

  export default {
    name: 'Home',

    components: {
      contenido,
    },
  }
</script>
<style scoped>
.home{
  width: 100%;
  height: 100%;
  /* background-color: #bed5f5c4; */
}

</style>
