<template>

<header class="BURGER">
  <h1> Welcome to the burgerplace of your dreams </h1>
  <img src = "/img/longburger.jpg">
</header>
<main>
  <a href="https://www.kebabhouseuppsala.se/"> KEBAB</a>
  <section class="BURGERTOWN">
    <h2> Choose the burger of your dreams </h2>
    <h3> This is where you choose your burger </h3>
    <nav> <b>Menu items</b>
    </nav>
    <div class="wrapper">
    </div>
      <div class="box a">
        <h4> Swedish MEATBALLMANIA </h4>
        <img src = "/img/bulle.jpg" style="width:200px">
        <ul>
          <li> 1000 calories </li>
            <li> <span class = "makebold"> Contains meat </span> </li>
              <li> Meatballs can be switched with falafel </li>
                <li> <span class = "makebold"> Contains gluten </span> </li>
                </ul>
                </div>
                <div class="box b">
                  <h4> INSANITY BURGER </h4>
                  <img src = "/img/insane.jpg" style="width:250px">
                  <ul>
                    <li> 2000 calories </li>
                      <li> <span class = "makebold"> Contains meat </span> </li>
                        <li> COW </li>
                          <li> Really good </li>
                          </ul>
                          </div>
                          <div class="box c">
                            <h4> CHICKEN ALLAN KING </h4>
                            <img src = "/img/chicken.jpg" style="width:250px">
                            <ul>
                              <li> 1200 calories </li>
                                <li> Only the best CHICKEN </li>
                                  <li> <span class = "makebold"> Contains gluten </span> </li>
                                  </ul>
                                  </div>
                                  </section>
                                  <section class="BURGERTOWN">
                                    <h2> Please provide with delivery information </h2>
                                    <h3> This is where you provide us with necessary information </h3>
                                    <label for="firstname">First</label><br>
                                    <input type="text" id="firstname" name="fn" required="required" placeholder="First name">
                                  <p>
                                    <label for="lastname">Last</label><br>
                                    <input type="text" id="lastname" name="ln" placeholder="Last name">
                                  </p>
                                  <p>
                                    <label for="Street">Street</label><br>
                                    <input type="Street" id="street" name="em" required="required" placeholder="Street adress">
                                  </p>
                                  <p>
                                    <label for="House">House</label><br>
                                    <input type="number" id="house number" name="em" required="required" placeholder="House number">
                                  </p>
                                  <p>
                                    <label for="Payment">Payment</label>
                                      <select id="Payment" name="rcp">
                                        <option selected="selected">Visa</option>
                                        <option>Mastercard</option>
                                        <option>American Express</option>
                                        <option>Swish</option>
                                        <option>Klarna</option>
                                      </select>
                                    </p>
                                    <p>Gender:</p>
                                    <div>
                                      <input type="radio" id="Female" name="drone" value="Female"
                                      checked>
                                      <label for="Female">Female</label>
                                    </div>
                                    <div>
                                      <input type="radio" id="Male" name="drone" value="Male">
                                      <label for="Male">Male</label>
                                    </div>
                                    <div>
                                      <input type="radio" id="Do not wish to provide" name="drone" value="Do not wish to provide">
                                      <label for="Do not wish to provide">Do not wish to provide</label>
                                    </div>
                                  </section>
                                  <br>
                                  <section class="BURGERTOWN">
                                    <button type="button">
                                      <img src="sendinfo.png">
                                    </button>
                                  </section>
                              </main>
                              <hr>
                              <section>
                                <footer>
                                  <p class="copyright">ALLANS BURGER BUNS © 2021</p>
                                </footer>
                              </section>
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
/* menyn ska vara här */

const socket = io();

function MenuItem (name, kCal, image, intolerant) {
this.name= name;
this.kalories = kCal;
this.url = image;
this.intolerans = intolerant;
}
const burgers = [
new MenuItem ("Swedish MEATBALLMANIA", 1000, "/img/bulle.jpg", "gluten" ),
new MenuItem (  "INSANITY BURGER",  2000,  "/img/insane.jpg",  false, false ),
new MenuItem ( "CHICKEN ALLAN KING", 1200,  "/img/chicken.jpg",  false, true )
];

console.log(burgers)
 /* Maybe add a form component */
export default {
name: 'Home',
components: {
Burger
},
data: function () {
return {
burgers: burgers /*[ {name: "", kCal: 250},
{name: "standard burger", kCal: 450},
{name: "large burger", kCal: 850}
]*/
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

@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';
@media screen and (max-width: 800px) {
    h1 {
        font-size: 6vw;
    }
}

body {
font-family: "Times New Roman", Times, serif; /* font-size: 12px; */
background-color: "white";
background-position: left;
}
.makebold {
      font-weight: bold;
}

#idname {
   text-transform: uppercase;
}
header h1 {
  position: absolute;
}
.BURGER {
  /* background-color: Black; color: White; */
  margin:10px;
  padding: 10px;
  border: 2px dashed yellow;
  opacity: 0.6;
  color: white;
  background-color: green;
  width: 500;
}
#Contact {

}

.wrapper {
  display: grid;
  grid-gap: 10px;
  margin-left: 10px;
  padding-top: 10px;
  padding-bottom: 10px;
  grid-template-columns: 280px 280px 280px 280px;
  background-color: orange;
  color: pink;
}
.box {
  background-color: green;
  color: #fff;
  border-radius: 10px;
  padding: 20px;
  font-size: 100%;
}


button:hover {
  background-color: red;
}

.BURGERTOWN {
  margin: 50px;
  padding: 20px;
  border: 2px dashed #ff0000;
  background-color: orange;
}

.button-margin {
  margin: 1px;
}

#map {
width: 300px;
height: 300px;
background-color: red;
}
</style>
