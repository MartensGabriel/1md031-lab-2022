<template>


<div>
  <header class = "image">

    <h1 class = "imagetext">
      Welcome to BurgerNation
    </h1>
  </header>

  <h2>Välj en burgare nedan</h2>
  Tryck på den burgaren du vill ha




  <main>
      <div class = "wrapper">

            <Burger v-for="burger in burgers"
                    v-bind:burger="burger"
                    v-bind:key = "burger.name"
                    v-on:selectedBurger="setSelectedBurger($event)"/>

      </div>

  <form>
    <section id="kontakt">
      <h3>
        Beställningsinformation
      </h3>
      <form>
        <p>
          <label for="Namn">För- och efternamn</label><br>
          <input type="text" id="fn" v-model="fn" required="required" placeholder="Namn">
        </p>
        <p>
          <label for="Mejladress">Mejladress</label><br>
          <input type="email" id="ma" v-model="ma" required="required" placeholder="Mejladress">
        </p>

<!--        <p>
          <label for="Adress">Gatunamn</label><br>
          <input type="Adress" id="sn" v-model="sn" required="required" placeholder="Adress">
        </p>
        <p>
          <label for="Husnummer">Husnummer</label><br>
          <input type="Adress" id="hn" v-model="hn" required="required" placeholder="Husnummer">
        </p>-->
      </form>
    </section>

    <section>
      <h3>Betalning</h3>

      <p>
        <label for="Betalningssätt">Betalningssätt: </label>
        <select id="pm" name="pm">
          <option selected = "selected"> Debit eller kredit </option>
          <option>Swish</option>
          <option>Paypal</option>
          <option>Klarna</option>
        </select>
      </p>

    </section>

    <section>
      <h3>
        Kön
      </h3>

      <input type="radio" id="gender" name="gender" value="Man">
      <label for="Man">Man</label><br>

      <input type="radio" id="gender" name="gender" value="Kvinna">
      <label for="Kvinna">Kvinna</label><br>

      <input type="radio" id="gender" name="gender" value="Annat">
      <label for="Annat">Annat</label><br>

    </section>
  </form>
  <h2>Tryck på leveransadressen </h2>
    <div id = "map">
      <div class ="map" id = "dots" v-on:click="setLocation">
        <div
          v-bind:style="{ left: this.CustomerInfo.location.x + 'px',
                        top: this.CustomerInfo.location.y + 'px'}">
          T
          </div>
      </div>
    </div>

      <br>
      <button class = "orderButton" type="submit" v-on:click="orderClick()">
        <img src="https://thumbs.dreamstime.com/b/nocamerasign-194400795.jpg" alt = "beställ" style="width:80px;height:80px;">
        Lägg beställning
      </button>






    <section>
      <h3>Customer information</h3>
      Adress: Ångströmsvägen 12
      <br>
      Mobil: 070333333
    </section>



  </main>


  <hr>
  <footer>
    &#169; BurgerNation 2022
    <br>
    Välkommen åter!!
  </footer>
  </div>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io();

const myMenu = menu;


/*function MenuItem(name, url, kcal, gluten, meat) {
  this.name = name;
  this.url = url;
  this.kcal = kcal;
  this.gluten = gluten;
  this.meat = meat;


}*/

//const burgare1 = new MenuItem("Enkel ostburgare","https://www.publicdomainpictures.net/pictures/180000/nahled/hearty-cheeseburger.jpg", "2000 kCal", "gluten", "nötkött");
//const burgare2 = new MenuItem("Dubbel ostburgare", "https://www.johansmat.se/wp-content/uploads/2018/11/smashed-cheeseburger.jpg", "2500 kCal", "gluten", "nötkött");
//const burgare3 = new MenuItem("Grov ostburgare", "https://preview.redd.it/c85s7560o6o41.jpg?auto=webp&s=702f63f195380ed5a430a0574d6e014a0d6d423b", "3000 kCal", "gluten", "nötkött");

//const burgerMenu = [burgare1, burgare2, burgare3];
const burgerMenu = [myMenu[0], myMenu[1], myMenu[2]];


export default {
  name: 'HomeView',
  components: {

    Burger
  },
  data: function () {
    return {
      burgers: burgerMenu,

      CustomerInfo: {
        selectedBurgers:[],
        fullName: "",
        mailAddress:"",
        //streetName:"",
        //houseNumber:"",
        paymentMethod:"",
        gender:"",
        location: {
          x: 0,
          y: 0
        }
      }
    }
  },
  methods: {

    setLocation: function(event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top};

      this.CustomerInfo.location.x = event.clientX -50 -offset.x;
      this.CustomerInfo.location.y = event.clientY -50- offset.y;
    },

    setSelectedBurger: function(event){

      for(let i = 0;i<this.CustomerInfo.selectedBurgers.length; i++) {
        console.log(this.CustomerInfo.selectedBurgers[i])
        if (this.CustomerInfo.selectedBurgers[i].name === event.name) {
          this.CustomerInfo.selectedBurgers[i].amount = event.amount
          if (event.amount == 0) {
            this.CustomerInfo.selectedBurgers.splice(i, 1)
          }
          return;
        }
      }




      this.CustomerInfo.selectedBurgers.push(event);
      console.log(this.CustomerInfo.selectedBurgers);
    },


    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};

      this.CustomerInfo.location.x = event.clientX -10 - offset.x;
      this.CustomerInfo.location.y = event.clientY -10 - offset.y;



    },
    orderClick: function() {
      this.CustomerInfo.fullName = document.getElementById("fn").value;
      this.CustomerInfo.mailAddress = document.getElementById("ma").value;
      //this.CustomerInfo.streetName = document.getElementById("sn").value;
      //this.CustomerInfo.houseNumber = document.getElementById("hn").value;
      this.CustomerInfo.paymentMethod = document.getElementById("pm").value;


      //Inspiration taget från; https://www.javatpoint.com/how-to-check-a-radio-button-using-javascript
      const genderChosen = document.getElementsByName("gender");
      const genderChecked = Array.from(genderChosen).find((radio)=>radio.checked);
      this.CustomerInfo.gender = genderChecked.value;


      console.log(this.CustomerInfo);

      socket.emit("addOrder", { orderId: this.getOrderNumber(),
            details: { x: this.CustomerInfo.location.x,
              y: this.CustomerInfo.location.y,
              fullName: this.CustomerInfo.fullName,
              mailAddress: this.CustomerInfo.mailAddress,
              paymentMethod: this.CustomerInfo.paymentMethod,
              gender: this.CustomerInfo.gender},
            orderItems: this.CustomerInfo.selectedBurgers
          }
      );
    }
  }
}
</script>

<style>
/*empty*/
/* Testkommentar */

body {
  font-family: Calibri;
  font-size: 20px;
  /*noinspection CssUnknownTarget*/
  background-image: url("https://media.istockphoto.com/vectors/seamless-op-art-80s-style-vector-wave-pattern-vector-id1140149373?k=20&m=1140149373&s=612x612&w=0&h=X_TAhGFEyUMpGsZcAvotcoyrbqL_9N9ovPuyz6bREZY=");
}




#kontakt {
  border-style: dashed;
  background-color: white;
}

button:hover {
  color: red;
  cursor: pointer;
}



.orderButton {
  margin: 80px;
  font-size: larger;
  background-color: darkcyan;
}

section {
  margin: 50px;
  background-color: white;
  border-style: dashed;
}

div {
  margin: 40px
}

.image {
  margin-left: 50px;
  margin-right: 50px;
  height: 300px;
  overflow: hidden;
  background-color: black;
  border-style: dotted; color: white;

}

.imagetext {
  position: absolute;
  top: 150px;
  width: 80%;
  margin: 0 auto;
  text-align:center;
  color: white;
  font-family: "Bauhaus 93";
  font-size: 60px;

}


.wrapper {
  display: inline-grid;
  grid-gap: 1px;
  grid-template-columns: 400px 400px 400px;
  justify-content: center;
  background-color: black;
  color: #444;

}



footer{
  background-color: white;
  border-style: dashed;
}

.map {
  width: 1920px;
  height: 1078px;
  background-image: url("@/assets/polacks.jpg");
  margin: auto;

}

#map {
  width: 1000px;
  height: 600px;
  overflow:scroll;
  margin:auto;
}



#dots div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}

</style>