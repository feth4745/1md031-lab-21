<template>
        <div :class="'box'+burger.ColumnNumber">
        <h3 class="burgername"> {{burger.name}}</h3>
        <img v-bind:src="burger.pic" style="width: 250px; height:140px;object-fit: cover">

            <ul>
                <li>Pris:{{burger.pris}}</li>
                <li v-if="burger.lactose">laktos</li>
                <li v-if="burger.gluten">gluten</li>
                <li>{{burger.kcal}} Kcal</li>
                <button v-on:click="minusBurger" id="minusButton" style="align-content: center">
                    -
                </button>
                {{amountOrdered}}
                <button v-on:click="plusBurger" id="plusButton" style="align-content: center">
                    +
                </button>
            </ul>
    </div>
</template>
<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  },
data: function () {
  return {
    amountOrdered: 0
  }
},
methods:{
    minusBurger: function (){
    this.amountOrdered-=1;
    if(this.amountOrdered<0){
        this.amountOrdered=0;
                }
    this.$emit('orderedBurger', 
            { name:   this.burger.name, 
            amount: this.amountOrdered 
            }
            );
    },
    plusBurger: function (){
    this.amountOrdered+=1;
    this.$emit('orderedBurger', 
            { name:  this.burger.name, 
            amount: this.amountOrdered 
            }
  );
  }
}}

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
#minusButton:hover{
        background-color:palevioletred;
    
    }
#plusButton:hover{
        background-color:#eafdec;
    }
</style>
