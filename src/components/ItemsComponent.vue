

<template>
          <div v-if="lessons">
        <ul class="lesson-boxes">
            <div v-for="lesson in lessons" class="lesson-box">
                <div class="left">
                    <img id="img"
                        v-bind:src="imageURL+lesson.topic+'.png'" />
                </div>
                <div class="right">
                    <p>Topic: <h2>{{ lesson.topic }}</h2></p>

                    <p>Location: <h2>{{ lesson.location }}</h2></p>

                    <p>Price: <h2>{{ lesson.price }}</h2></p>

                    <p v-if="lesson.space <= 0">No more spaces!</p>
                    <p v-else-if="lesson.space <= 5">Only<b> {{lesson.space}}</b> spaces!</p>
                    <p v-else> Spaces:<h2> {{lesson.space}}</h2></p>

                    <input class="basketbt" type="button" value="Add to Basket" v-on:click="toBasket(lesson)"
                        v-if="lesson.space > 0" />
                    <input class="basketbt" type="button" value="Add to Basket" disabled="disabled" v-else />
                </div>
            </div>
        </ul>
    </div>
    <div v-else>Loading data</div>
</template>

<script>
export default{
  name:"lessons",
  props:["lessons","imageURL"],
  data(){
    return{}
  },
  methods: {
    toBasket:function (lesson){ 
      this.$emit("to-Basket",lesson);
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


@media (min-width: 1024px) {
  .basketbt{
    position: absolute;
    bottom: 0px;
    right: 30px;
  }
}
</style>
