

<template>
          <div v-if="lessons">
        <ul class="lesson-boxes">
            <div v-for="lesson in lessons" class="lesson-box">
                <div class="left">
                    <img id="img"
                        v-bind:src="imageURL+lesson.topic+'.png'" />
                </div>
                <div class="right">
                    <p>Topic: <b>{{ lesson.topic }}</b></p>
                    <p>Location: <b>{{ lesson.location }}</b></p>
                    <p>Price: <b>{{ lesson.price }}</b></p>
                    <p v-if="lesson.space <= 0">No more spaces!</p>
                    <p v-else-if="lesson.space <= 5">Only<b> {{lesson.space}}</b> spaces!</p>
                    <p v-else> Spaces:<b> {{lesson.space}}</b></p>
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

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    display: block;
    text-align: left;
  }
}
</style>
