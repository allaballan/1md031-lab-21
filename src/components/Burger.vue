<template>

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
.box {
  background-color: green;
  color: #fff;
  border-radius: 10px;
  padding: 20px;
  font-size: 100%;
}

</style>
