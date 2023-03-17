<template>
      <div v-if="cart.length > 0">
        <div>
            <div class="cart" >
                <div class="mini-cont">
                  <h2> Shopping Cart </h2>
                    <p>Items in cart: <b>{{cart.length}}</b></p>
                    <p>Total Price: <b>{{totalPrice}}</b></p>
                </div>
                <div class="itemsCont">
                    <div v-for="item in cart" class="cont-mini">
                        <h3 style="float: left; width: 33%;">Topic: {{item.topic}} </h3>
                        <p style="float: left; width: 33%;">Location: {{item.location}}</p>
                        <p style="float: right; width: 30%;">Price: {{item.price}}</p>
                        <input class="basketbt" type="button" value="Remove" v-on:click="remove(item)" />
                    </div>
                </div>
                <div class="form">

                <div class="input-container">
                    <input type="text" id="name" placeholder=" " v-model="checkout.name">
                    <label for="name">Name:</label>
                </div>

                <div class="input-container">
                    <input type="number" id="phone" placeholder=" " v-model="checkout.phone">
                    <label for="phone">Phone:</label>
                </div>
                <div id="feedback">
                    <p></p>
                </div>
                <button v-on:click="placeOrder()" type="button" class="basketbt">Place order</button>
                
            </div>
            </div>
        </div>
      </div>
      <div v-else><h1 style="margin-top: 100px;">Cart empty</h1></div>
</template>

<script>
export default {
  name: "cart",
  props: ["cart","totalPrice"],
  data() {
    return {}
  },
  methods: {
    remove:function (lesson){ 
      this.$emit("removE",lesson);
    }
  }
}
</script>
<style scoped>
h1 {
font-weight: 500;
font-size: 2.6rem;
top: -10px;
}

h3 {
font-size: 1.2rem;
}
.mini-cont{
  text-align: center;
}
.cart{
  width: 100%;
}
@media (min-width: 1024px) {
.basketbt{
position: absolute;
bottom: 0px;
right: 30px;
}
.cart{
  width: 50%;
}
}
</style>
