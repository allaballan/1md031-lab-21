<template>
  <div id="orders">
    <div id="orderList">
      <div v-for="(order, key) in orders" v-bind:key="'order'+key">
        <h2 class = "yourOrder">  #{{ key }} </h2>
        <p class="yourOrder"> Beställda burgare: </p>
        {{order.orderItems}}
        <br>
        <p class="yourOrder"> Information </p>
        {{order.information.firstname}}
        {{order.information.lastname}},
        <br>
        {{order.information.email}},
        <br>
        {{order.information.rcp}},
        <br>
        {{order.information.gender}})
        <br>
      </div>
      <button v-on:click="clearQueue">Clear Queue</button>
    </div>
    <div id="dots">
      <div v-for="(order, key) in orders"
           v-bind:style="{ left: order.details.x + 'px', top: order.details.y + 'px'}"
           v-bind:key="'dots' + key">
        {{ key }}
      </div>
    </div>
  </div>
</template>
<script>
import io from 'socket.io-client'
const socket = io();

export default {
  name: 'Dispatcher',
  data: function () {
    return {
      orders: null
    }
  },
  created: function () {
    socket.on('currentQueue', data =>
        this.orders = data.orders);
  },
  methods: {
    clearQueue: function () {
      socket.emit('clearQueue');
    }
  }
}
</script>
<style>

@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';


#orderList {
  width: 400px;
  top:1em;
  left:1em;
  position: absolute;
  z-index: 2;
  background: rgba(255,255,255, 0.5);
  padding: 1em;
  font-weight: bold;
  font-family: "Kristen ITC"; /* font-size: 12px; */
  color: black;
  text-underline-color: white;

}
#dots {
  position: relative;
  margin: 0;
  padding: 0;
  background: url(/img/polacks.jpg);
  background-repeat: no-repeat;
  width:1920px;
  height: 1078px;
  cursor: crosshair;
}

#dots div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
  font-weight: bold;
}

#yourOrder {
  font-weight: bold;
}
</style>
