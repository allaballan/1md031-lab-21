<template>

  <header class="header">
    <h1> Welcome to the burgerplace of your dreams </h1>
    <img src = "/img/longburger.jpg">
  </header>


  <main>
    <section class="decide">
      <h2> Choose the burger of your dreams </h2>
      <h3> This is where you choose your burger </h3>
      <nav> <b>Menu items</b>
      </nav>

      <div class="burgers">
        <Burger v-for="burger in burgers"
                v-bind:burger="burger"
                v-bind:key="burger.name"
                v-on:burgerOrdered = "addToOrder ($event)"/>
      </div>
    </section>

    <section class="pinfo">
      <h2> Please provide with delivery information </h2>
      <h3> This is where you provide us with necessary information </h3>

      <label for="firstname">First</label><br>
      <input type="text" id="firstname" v-model="firstname" required="required" placeholder="First name">
      <p>
        <label for="lastname">Last</label><br>
        <input type="text" id="lastname" v-model="lastname" placeholder="Last name">
      </p>"
      <p>
        <label for="Street">Street</label><br>
        <input type="Street" id="street" v-model="sn" required="required" placeholder="Street adress">
      </p>
      <p>
        <label for="House">House</label><br>
        <input type="number" id="house number" v-model="hn" required="required" placeholder="House number">
      </p>
      <p>
        <label for="Payment">Payment</label>
        <select id="Payment" v-model="rcp">
          <option selected="selected">Visa</option>
          <option>Mastercard</option>
          <option>American Express</option>
          <option>Swish</option>
          <option>Klarna</option>
        </select>
      </p>
      <p>Gender:</p>
      <div>
        <input type="radio" id="Female" v-model="drone" value="Female"
               checked>
        <label for="Female">Female</label>
      </div>
      <div>
        <input type="radio" id="Male" v-model="drone" value="Male">
        <label for="Male">Male</label>
      </div>
      <div>
        <input type="radio" id="Do not wish to provide" v-model="drone" value="Do not wish to provide">
        <label for="Do not wish to provide">Do not wish to provide</label>
      </div>
    </section>

    <label>  </label>
    <div id = "wrap">
      <div id = "map" v-on:click="setLocation"></div>
      <div id ="T" v-bind:style="{left:location.x + 'px', top: location.y + 'px'}">
        T
      </div>
    </div>

    <br>

      <button v-on:click = "submiter" type = "submit">
        <p> Click here to place your order</p>
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2FUSPzuaNQqKbZXG8V1Ijk7RYCZaP4kB78Q&usqp=CAU">
      </button>

  </main>
  <hr>
  <section>
    <footer>
      <p class="copyright">ALLANS BURGER BUNS © 2021</p>
    </footer>
  </section>

</template>

<script>
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io();

/*
function MenuItem (name, kCal, image, gluten, lactose) {
this.name= name;
this.kCal = kCal;
this.image = image;
this.gluten = gluten;
this.lactose = lactose;
} */
/*
const burgers = [
new MenuItem ("Swedish MEATBALLMANIA", 1000, "/../img/bulle.jpg", false, true ),
new MenuItem (  "INSANITY BURGER",  2000,  "/../img/insane.jpg",  true, false ),
new MenuItem ( "CHICKEN ALLAN KING", 1200,  "/../img/chicken.jpg",  false, true )
];
*/
console.log()

/* Maybe add a form component */
export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu,
      drone: "",
      burgerOrdered: [],
      location: "",

    }
  },

  methods: {

    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },

    addToOrder: function (event) {
      this.burgerOrdered[event.name] = event.amount;
      console.log(this.burgerOrdered)
    },

    setLocation: function (event) {
      const offset = event.target.getBoundingClientRect();
      this.location.x = event.clientX - offset.left - 10;
      this.location.x = event.clientX - offset.top - 10;

    },

    submiter: function () {
      socket.emit("addOrder", {
            orderId: this.getOrderNumber(),
            details: {
              x: this.location.x,
              y: this.location.y
            },
            orderItems: ["Beans", "Curry"]
          },
      );
    },
    addOrder: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top
      };
      socket.emit("addOrder", {
            orderId: this.getOrderNumber(),
            details: {
              x: event.clientX - 10 - offset.x,
              y: event.clientY - 10 - offset.y
            },
            orderItems: ["Beans", "Curry"]
          },
      );
    }
  }
}


</script>

<style>

@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';
@media screen and (max-width: 800px) {
  h1 {
    font-size: 6vw;
  }
}

body {
  font-family: "Times New Roman", Times, serif; /* font-size: 12px; */
  background-color: white;
  background-position: left;
}

header img{
  width: 100%;
  height: 300px;
  opacity: 0.6;
}

.pinfo {
  background-color: orange;
  color: white;
  font-size: 10px;
  margin: 10px 10px 10px 10px;
  border: 2px dashed black;
  padding-left: 10px;
  width: 1000px
}

header h1 {
  position: absolute;
  color: black;
}

button {
  margin-top: 20px;
  margin-bottom: 10px;
}

button:hover {
  background-color: red;
  cursor: alias;
}

.decide {
  width: 1300px;
  height: 800px;
  margin: 20px;
  background-color: black;
  color: white;
}

.burgers {
  display: grid;
  grid-gap: 40px;
  grid-template-columns: auto auto auto;
  color: white;
}

#map {
  width: 1920px;
  height: 1078px;
  background: url("/img/polacks.jpg");
}

#wrap {
  width: auto;
  height: 500px;
  overflow:scroll;
  position: relative;
}

#T {
  position: absolute;
  color: black;
  border-radius: 10px;
  width: 20px;
  height: 20px;
  color: pink;
}


</style>