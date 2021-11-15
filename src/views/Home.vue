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

function MenuItem (name, kCal, image, intolerant) {
this.burger= name;
this.url = image;
this.kalories = kCal;
this.allergi = intolerant;
}

const burgers = [
New MenuItem =  ("Swedish MEATBALLMANIA", 1000, "/img/bulle.jpg", "gluten" ),
New MenuItem =  ( name: "INSANITY BURGER", kCal: 2000, url: "/img/insane.jpg", lactose: false, gluten: false ),
New MenuItem =  ( name: "CHICKEN ALLAN KING", kCal: 1200, url: "/img/chicken.jpg", lactose: false, gluten: true )
]

console.log(burgers)

export default {
  name: 'Home',
  components: {
    Burger
  },
  data: burgers (name, kCal, image, intolerant) {
    return {
      burgers: [ {name: "small burger", kCal: 250},
                 {name: "standard burger", kCal: 450},
                 {name: "large burger", kCal: 850}
               ]
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
