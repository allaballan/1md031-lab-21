<template>

  <div class="burgers">
    <h4> {{burger.name}} </h4>
    <img v-bind:src = "burger.image">
    <ul>
      <li> {{burger.kCal}} </li>
      <li> {{burger.gluten}}</li>
      <li> {{burger.lactose}}</li>
    </ul>
  </div>

  <section class = "orders"> Orders: {{orderedAmount}}</section>

  <button v-on:click = "minusBurger" class = "menos">
    -1
  </button>

  <button v-on:click = "plusBurger" class = "mas">
    +1
  </button>

  
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  },
  data: function () {
    return {
      orderedAmount: 0
    }
  },
  methods: {
    minusBurger: function() {
      this.orderedAmount -= 1;
      if(this.orderedAmount < 0) {
        this.orderedAmount = 0;
      }
      this.$emit("burgerOrdered", {
        name:this.burger.name,
        amount: this.orderedAmount
      });
    },
    plusBurger: function() {
      this.orderedAmount += 1;
      this.$emit("burgerOrdered", {
        name:this.burger.name,
        amount: orderedAmount
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.burgers {
  background-color: green;
  color: #fff;
  border-radius: 10px;
  padding: 20px;
  font-size: 100%;
}

</style>
