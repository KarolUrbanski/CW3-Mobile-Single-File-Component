<script setup>
import ItemsComponent from "./components/ItemsComponent.vue";
import CartComponent from "./components/CartComponent.vue";
</script>

<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <button id="cartBTN" @click="showCheckout">{{ this.cart.length }} 
            <font-awesome-icon icon="fa-solid fa-cart-shopping" />
            Cart
          </button>

          <div class="searchBox">
              <input class="searchInput" type="text" placeholder="Search" v-model.trim="searchString" @keyup="getLessons">
              <button class="searchButton" href="#">
                <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
              </button>
            </div>
    </header>

    <main>
      <component :is="currentView" :lessons="lessons" :imageURL="imageURL" @to-Basket="toBasket"
      :cart="cart" :totalPrice="totalPrice" @removE="remove">
      </component>
    </main>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      sitename: "After School Club",
      lessons: [],
      searchString: '',
      serverURL:"https://webstoreapp-env.eba-z8zi99ic.us-east-1.elasticbeanstalk.com/lessons/products",
      imageURL:"https://webstoreapp-env.eba-z8zi99ic.us-east-1.elasticbeanstalk.com/static/",
      cart: [],
      currentView: ItemsComponent
    }
  },

  components: { ItemsComponent, CartComponent },
  methods: {
    toBasket: function (subjec) {
                    //add subject to basker array
                    this.cart.push(subjec);
                    this.cart.count += 1;
                    subjec.space -= 1;
                },

    showCheckout() {
      if (this.currentView === ItemsComponent) {
        this.currentView = CartComponent;
      }
      else {
        this.currentView = ItemsComponent;
      }
    },
    remove: function (subjec) {
                    //for every element in order
                    for (var i = 0; i < this.cart.length; i++) {
                        //check for first id to remove
                        if (this.cart[i] == subjec) {
                            //remove subject/count add spaces and return to not remove all the same objects
                            this.cart.splice(i, 1);
                            subjec.space += 1;
                            return
                        }
                    }
                },

    getLessons () {
      let webstore=this;
      let searchStringLower = this.searchString.toLowerCase();
      console.log(searchStringLower)

                if (!searchStringLower) {
                fetch(this.serverURL, {
                    method: 'GET',
                    //  mode: 'no-cors',
                    headers: {
                        "Content-Type": "application/json",
                    }
                }).then(
                    function (response) {
                        response.json().then(function (json) {
                            webstore.lessons=json;
                        })
                    }
                )
                }
                else{
            fetch(this.serverURL+"/"+searchStringLower, {
                    method: 'GET',
                    //  mode: 'no-cors',
                    headers: {
                        "Content-Type": "application/json",
                    }
                }).then(
                    function (response) {
                        response.json().then(function (json) {
                          webstore.lessons=json;
                        })
                    }
                )
 
            }
            }
  },
  computed: {
    totalPrice: function () {
                    //calculate total price
                    let total = 0;
                    this.cart.forEach(subj => {
                        total = total + subj.price;
                    });
                    return total;
                },

  },
  created: function(){
    if ("serviceWorker" in navigator) {
              navigator.serviceWorker.register("service-worker.js");
        }
    this.getLessons();
    
        }
};
</script>

<style scoped>
header {
  line-height: 1.5;
}
#cartBTN{
cursor:pointer;
font-size:24px;
position: absolute;
right: 10px;
top:5px;
border: none;
color: white;
background-color: transparent;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
  #cartBTN{
font-size:28px;
}
}
</style>
