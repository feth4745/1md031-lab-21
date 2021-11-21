<template>

<header> 
            <section>
                <h1>Marx</h1> 
                <h2>Hamburgare</h2>
                <img src="https://www.nordangliaeducation.com/-/media/corporate/our-schools/city-page-images/moscow.jpg?h=489&iar=0&w=1920&hash=5145FECA9246781FDA620EFC9593D785" alt="span" title="workersofallcountriesunite" class="borderpicture">
            </section>
        </header>
        <section class="meals">
            
            <h2 class="headline">Välj din burgare:</h2>
                <div class="wrapper">
                    <Burger v-for="burger in burgers"
                    v-bind:burger="burger"
                    v-bind:key="burger.name"
                    v-on:orderedBurger="addToOrder($event)"/>
            </div>
            
        </section>
       
        <main>
        
        <section>
        <h3 class="name" id="kundinfo" style="text-align: center;">Kundinformation: </h3>
        </section>
            
            <section id="contact" style="text-align: center">
                <form>
                <div class="wrapper2">
                <div class="fyrkant a">
                <p>
                <label for="Full Name">Full Name</label><br>
                    <input type="text" id="fullname" v-model="fullName" required="required" placeholder="Name">
                </p>
                <p>
                    <label for="">Epost-adress</label><br>
                    <input type="email" id="email" v-model="email" required="required" placeholder="E-mail address">
                </p>
                 <p>
                <label for="">Street Name</label><br>
                <input type="text" id="street name" v-model="streetName" placeholder="street name">
                </p>
                 <p>
                    <label for="">House Number</label><br>
                    <input type="number" id="lastname" v-model="houseNumber" placeholder="house number">
                </p>
                    </div>
                    <br/>
                    <div class="fyrkant b">
                    
                    <div id="väljkön" class="kundinfo">
                <select v-model="selected">
                        <option disabled value="">Kön:</option>
                        <option>Vill ej uppge</option>
                        <option>Man</option>
                        <option>Kvinna</option>
                </select>
                        </div> 
                    
                
                    
                    </div> 
                    </div>
                </form>
            </section>
            <div class="map" style="width:300px;height: 300px; overflow:scroll">
                    <div id="map" v-on:click="addOrder" >
                    Drop point:
                    </div>
                    </div>
            <section style="text-align: center;">
            <button v-on:click="sendOrder" style="align-content: center">
  <img src="https://www.nusr-et.com.tr/nusret_files/2016223144139545_burger.png" style="width: 25px">
  Send Order
</button>
    
    </section>
        </main>
       
        <br />
        
       <footer>
        &copy;
       </footer>
</template>

<script>
import Burger from '../components/Burger.vue'
    import menu from '../assets/menu.json'
import io from 'socket.io-client'

const socket = io();

/*
function MenuItem(name, pic, kcal, gluten, lactose, number){
    this.name=name;
    this.pic=pic;
    this.kcal=kcal;
    this.gluten=Boolean(gluten);
    this.lactose=Boolean(lactose);
    this.ColumnNumber="box"+number%3;
    
}
    

const burgers=[
                new MenuItem("The beorgeoisie burger","https://cdn-bk-se-ordering.azureedge.net/media/x0ljohbg/bk-kiosk-checkout-machine-400x290_singel_roasted_onion_singlebeef.png","700",true,true,1),
                new MenuItem("The Soviet burger", "https://dabas.blob.core.windows.net/media/danora-sweden/12191%20toast_skinke_ost%20lavoppl%C3%B8selig.jpg", "300",false,false,2),
                new MenuItem("The peasant burger","https://www.mcdonalds.com/is/image/content/dam/usa/nfl/nutrition/items/hero/desktop/t-mcdonalds-Cheeseburger.jpg?$Product_Desktop$", "380", false,true,3)
]
*/
    
export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
            burgers: menu,
            orderedBurgers:{"The beorgeoisie burger":0, "The Soviet burger":0, "The peasant burger":0}
    }
  },
  methods: {
    sendOrder: function() {
    console.log(this.houseNumber)
    
          
    },
    addToOrder: function (event) {
    this.orderedBurgers[event.name] = event.amount;
    console.log(this.orderedBurgers)
    },
    
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
    width: 1920px;
    height: 1078px;
    background: url("/img/polacks.jpg");
  }
    .map:hover{
        cursor:pointer;
    }

@import 'https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap';
@import 'https://fonts.googleapis.com/css2?family=Abel&display=swap';
.borderpicture{ 
            opacity: 1;
            width: 100%;
}

header h1{
        position:absolute;
        margin-top: 0.75em;
        margin-left: 6em;
        font-family: "Abril Fatface";
        font-size: 5em;
        color: red;
}
header h2{
        position:absolute;
        margin-top: 1.6em;
        margin-left: 4.8em;
        font-family: "Abril Fatface";
        font-size: 5em;
        color: black;
}
header{
        margin: auto;
        margin-bottom:0;
        height:auto;
        overflow:hidden;
        
}
body{
    color:black;
    font-family: Abel;
    
    
}/*empty*/
body li{
    font-size: 19px;
}
body .headline{
            font-size: 42px;
}
.name{
        font-size: 30px;
        color: black;
    
}
.meals{
        background-color: white;
        color:black;
    
}
.headline{
    font-size: 36px;
    font-weight: 700;
    text-align: center;
}
body ul{
        list-style-type: circle;
        
}

button:hover{
    background-color: #eafdec;
    cursor:pointer;
}
    v
button{
        margin-left:3em;
}
section{
        margin:2em;
        margin-top:0;
}
.wrapper { 
    display: grid;
    grid-gap: 5px;
    grid-template-columns: 315px 315px 315px;
    background-color: white;
    color: white;
    justify-content:center;
    
    }
 .box {
     background-color: white;
     color: black;
     border-radius: 5px;
     padding: 20px;
     font-size: 150%;
 }
</style>
