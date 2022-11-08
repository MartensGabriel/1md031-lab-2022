<template>
  <div class="box" >
    <h3>{{burger.name}}</h3>
    <img v-bind:src="burger.url" style = "width:200px;height:200px;">
    <ul>
      <li>
        {{burger.kcal}}
      </li>
      <li class = "gluten">
        {{burger.gluten}}
      </li>
      <li>
        {{burger.meat}}
      </li>
    </ul>
  </div>
</template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  body {
    font-family: Calibri;
    font-size: 20px;
  }

  .gluten {
    color: #ff5500;
    text-transform: uppercase;
  }


  .box {
    background-color: #444;
    color: #fff;
    border-radius: 5px;
    padding: 20px;
    font-size: 150%;
  }
  </style>
  