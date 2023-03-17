<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
</script>

<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <button @click="showCheckout">{{ this.cart.length }} Checkout</button>
      <img
        alt="Vue logo"
        class="logo"
        src="./assets/logo.svg"
        width="125"
        height="125"
      />
    </header>

    <main>
      
      <component :is="currentView">
        
      </component>
    </main>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      sitename: "Vue.js Pet Depot",
      cart: [],
      currentView: HelloWorld
    }
  },

  components: { HelloWorld, HelloWorld },
  methods: {
    showCheckout() {
      if (this.currentView === HelloWorld) {
        this.currentView = TheWelcome;
      }
      else {
        this.currentView = HelloWorld;
      }
    }
  }
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
