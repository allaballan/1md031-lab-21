<template>

  <div>

    <section class = "burgers">

      <div>
        <h4> {{burger.name}} </h4>
        <img v-bind:src = "burger.image" class="bilder">
        <ul>
          <li>{{ burger.kCal }} kCal</li>
          <li v-if = "burger.lactose" id = "lactose"> Contains <span> lactose </span></li>
          <li v-if = "burger.gluten" id = "gluten"> Contains <span> gluten </span></li>
          <li>{{ burger.line1 }}</li>
          <br>
          <p> Amount ordered: {{orderedAmount}}</p>
        </ul>

        <button v-on:click = "plusBurger" class = "mas">
          +1
        </button>

        <button v-on:click = "minusBurger" class = "menos">
          -1
        </button>
      </div>
    </section>
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
      orderedAmount: 0,
    }
  },
  methods: {
    minusBurger: function() {
      this.orderedAmount -= 1;
      if(this.orderedAmount < 0) {
        this.orderedAmount = 0;
      }
      this.$emit("burgerOrdered", {
        name: this.burger.name,
        amount: this.orderedAmount,
        location: {x: 0, y: 0}
      });
    },
    plusBurger: function() {
      this.orderedAmount += 1;
      this.$emit("burgerOrdered", {
        name:this.burger.name,
        amount: this.orderedAmount,
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

body {
  font-family: "Times New Roman", Times, serif;
  font-size: 10px;
  display: grid !important;
  grid-gap: 10px !important;
}

h4 {
  font-size: 2em !important;
  width: 100%;
  text-align: center;
}

button {
  margin-left: 5px;
  width: 50px;
  height: 50px;
  align-content: center;
}

.mas {
  background-color: yellow;
}

.menos {
  background-color: green;
}

.bilder {
  height: 250px;
  width: 250px;
}

</style>
