<template>
    
        <h3 class="burgername"> {{burger.name}}</h3>
        <img v-bind:src="burger.pic" style="width: 250px; height:140px;">

            <ul>
                <li>pris</li>
                <li>Gluten</li>
                <li>Laktos</li>

            </ul>
</template>
<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
