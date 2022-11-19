<template>
  <div class="box" >
    <h3>{{burger.name}}</h3>
    <img v-bind:src="burger.url" style = "width:200px;height:200px;">
    <ul>
      <li>
        {{burger.kcal}}
      </li>
      <li class = "glutenMeat">
        {{burger.gluten}}
      </li>
      <li class = "glutenMeat">
        {{burger.meat}}
      </li>
    </ul>
    <button v-on:click="selectThisBurger"> select </button>
    <button v-on:click= "unSelectThisBurger"> unselect</button>
    Antal: {{ amountOrdered }}
  </div>
</template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    },
    data: function() {
      return {

        amountOrdered: 0,
      }
    },




   methods: {
       selectThisBurger: function(){
         this.amountOrdered+=1;
         this.$emit("selectedBurger", {name: this.burger.name, amount: this.amountOrdered})
         //console.log(this.burger.name, this.amountOrdered)
       },
       unSelectThisBurger: function() {
         if (this.amountOrdered >0)
           this.amountOrdered-=1;
         else return this.amountOrdered
         this.$emit("unSelectedBurger", {name: this.burger.name, amount: this.amountOrdered})

         //console.log(this.burger.name, this.amountOrdered)
       }
     }
   }


  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  body {
    font-family: Calibri;
    font-size: 20px;
  }

  .glutenMeat {
    color: #ff5500;
    text-transform: uppercase;
  }


  .box {
    background-color: #444;
    color: #fff;
    border-radius: 6px;
    padding: 15px;
    font-size: 150%;
  }

  </style>
  