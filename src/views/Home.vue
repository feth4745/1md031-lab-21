<template>
  <div>
    Burgers
    <Burger v-for="burger in burgers"
            v-bind:burger="burger" 
            v-bind:key="burger.name"/>
  </div>
  <div id="map" v-on:click="addOrder">
    click here
  </div>
  
</template>

<script>
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'
const socket = io();

function MenuItem(n,url,kcal,gluten,lactose){
    this.name=n;
    this.url=url;
    this.kcal=kcal;
    this.gluten=Boolean(gluten);
    this.lactose=Boolean(lactose);
}
const burgarlista=[new MenuItem("Burgare1","pic",300,false,false), new MenuItem("Burgare2","pic2",400,true,false), new MenuItem("Burgare3","pic3",450,false,true)];

export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: burgarlista
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }
</style>