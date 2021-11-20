<template>
        <div :class="'box'+burger.ColumnNumber">
        <h3 class="burgername"> {{burger.name}}</h3>
        <img v-bind:src="burger.pic" style="width: 250px; height:140px;object-fit: cover">

            <ul>
                <li>pris</li>
                <li>gluten</li>
                <li>laktos</li>

            </ul>
    </div>
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
.burgername{
        font-size: 30px;
        color: black;
    
}
ul{
        font-size:21px;
        color:black;
    }
</style>
