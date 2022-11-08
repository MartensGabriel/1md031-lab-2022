<template>

  <div>
  <header class = "image">

    <h1 class = "imagetext">
      Welcome to BurgerNation
    </h1>
    <img id = "kossa" src="https://www.dartagnan.com/on/demandware.static/-/Sites-dartagnan-Library/default/dw3d232de5/images/content/what-is-wagyu-beef.jpg?sw=660&strip=false" alt="Startsida">


  </header>

  <h2>Välj en burgare nedan</h2>
  Tryck på den burgaren du vill ha



  <main>
    <section id = "menyn">
      <div class = "wrapper">
        <div class="box a">
          <h3>Enkel ostburgare</h3>
          <img src = "https://www.publicdomainpictures.net/pictures/180000/nahled/hearty-cheeseburger.jpg" alt = "enkelburgare" style = "width:200px;height:200px;">
          <ul>
            <li>
              Isbergsallad
            </li>
            <li>
              90 g Wagyu puck
            </li>
            <li>
              En ostskiva
            </li>
            <li>
              Omslutet av Brioche
            </li>
            <li class = "gluten">
              Innehåller gluten och kött
            </li>
          </ul>
        </div>

        <div class="box b">
          <h3>Dubbel ostburgare</h3>
          <img src = "https://www.johansmat.se/wp-content/uploads/2018/11/smashed-cheeseburger.jpg" alt = "dubbelburgare" style="width:200px;height:200px;">
          <ul>
            <li>
              Isbergsallad
            </li>
            <li>
              2 x 90 g Wagyu puck
            </li>
            <li>
              2 x En ostskiva
            </li>
            <li>
              Omslutet av Brioche
            </li>
            <li class = "gluten">
              Innehåller gluten och kött
            </li>
          </ul>
        </div>

        <div class="box c">
          <h3>Grov ostburgare</h3>
          <img src = "https://preview.redd.it/c85s7560o6o41.jpg?auto=webp&s=702f63f195380ed5a430a0574d6e014a0d6d423b" alt = "dubbelburgare" style = "width:200px;height:200px;">
          <ul>
            <li>
              Isbergsallad
            </li>
            <li>
              3 x 90 g Wagyu puck
            </li>
            <li>
              3 x En ostskiva
            </li>
            <li>
              Omslutet av Brioche
            </li>
            <li class = "gluten">
              Innehåller gluten och kött
            </li>
          </ul>
        </div>

      </div>
    </section>

    <section id="kontakt">
      <h3>
        Beställningsinformation
      </h3>
      <form>
        <p>
          <label for="Namn">För- och efternamn</label><br>
          <input type="text" id="Namn" name="fn" required="required" placeholder="Namn">
        </p>
        <p>
          <label for="Mejladress">Mejladress</label><br>
          <input type="email" id="Mejladress" name="em" required="required" placeholder="Mejladress">
        </p>

        <p>
          <label for="Adress">Gatunamn</label><br>
          <input type="Adress" id="Adress" name="em" required="required" placeholder="Adress">
        </p>
        <p>
          <label for="Husnummer">Husnummer</label><br>
          <input type="Adress" id="Husnummer" name="em" required="required" placeholder="Husnummer">
        </p>
      </form>
    </section>

    <section>
      <h3>Betalning</h3>

      <p>
        <label for="Betalningssätt">Betalningssätt: </label>
        <select id="Betalningssätt" name="rcp">
          <option>Debit- eller kreditkort</option>
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

      <input type="radio" id="Man" name="fav_language" value="Man" checked = "checked">
      <label for="Man">Man</label><br>

      <input type="radio" id="Kvinna" name="fav_language" value="Kvinna">
      <label for="Kvinna">Kvinna</label><br>

      <input type="radio" id="Annat" name="fav_language" value="Annat">
      <label for="Annat">Annat</label><br>

    </section>

    <section>
      <br>
      <button type="submit">
        <img src="https://thumbs.dreamstime.com/b/nocamerasign-194400795.jpg" alt = "beställ" style="width:30px;height:30px;">
        Lägg beställning
      </button>
    </section>



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

const socket = io();

function MenuItem(name, url, kcal, gluten, meat) {

  this.name = name;
  this.url = url;
  this.kcal = kcal;
  this.gluten = gluten;
  this.meat = meat;
}

const burgare1 = new MenuItem("Enkel ostburgare","https://www.publicdomainpictures.net/pictures/180000/nahled/hearty-cheeseburger.jpg", "2000 kCal", "gluten", "kött");
const burgare2 = new MenuItem("Dubbel ostburgare", "https://www.johansmat.se/wp-content/uploads/2018/11/smashed-cheeseburger.jpg", "2500 kCal", "gluten", "kött");
const burgare3 = new MenuItem("Grov ostburgare", "https://preview.redd.it/c85s7560o6o41.jpg?auto=webp&s=702f63f195380ed5a430a0574d6e014a0d6d423b", "3000 kCal", "gluten", "kött");
const Menu = [burgare1, burgare2, burgare3];


export default {
  name: 'HomeView',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    Burger
  },
  data: function () {
    return {
      burgers: Menu
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
/*empty*/
/* Testkommentar */

body {
  font-family: Calibri;
  font-size: 20px;
}

.gluten {
  color: #ff5500;
  text-transform: uppercase;
}


#menyn {
  background-color: black;
  color: white
}

#kontakt {
  border-style: solid;
}

button:hover {
  color: red;
  cursor: pointer;
}

button{
  margin: 30px;
}

section {
  margin: 50px;
}

div {
  margin: 40px
}

.image {
  margin-left: 50px;
  margin-right: 50px;



  height: 300px;
  overflow: hidden;

}

.imagetext {
  position: absolute;
  top: 150px;
  width: 100%;
  margin: 0 auto;
  text-align:center;

}

#kossa {
  width: 100%;
  height: auto;
  opacity: 0.5;

}

.wrapper {
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 350px 350px 350px;
  background-color: black;
  color: #444;
}

.box {
  background-color: #444;
  color: #fff;
  border-radius: 5px;
  padding: 20px;
  font-size: 150%;
}

.a {
  grid-column: 1 ;
}
.b {
  grid-column: 2 ;
}
.c {
  grid-column: 3 ;
}

</style>