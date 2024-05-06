<template>
  <div class="app" >
    <Carousel class="carousel" :current-slide="currentSlide">
      <Slide v-for="index in 4" :key="index">
        <div v-show="currentSlide === index" class="slide-info" v-if="index === 1">
          <p>What's my favorite line of the Shrek movie?</p>
        </div>

        <div v-show="currentSlide === index" class="slide-info" v-else-if="index === 2">
          <p>Choose your favorite date: <br> </p>
          <input type="date" v-model="selectedDate" class="date-input">
        </div>

        <div v-show="currentSlide === index" class="slide-info" v-else-if="index === 3">
          <div class="flexbox-container">
            <div class="flex-1">Imagine creating layouts with floats and positioning...</div>
            <div class="flex-2">Why is the Shrek script here?</div> 
            <div class="flex-3">I was hoping there would be free bitcoin :(</div>
            <div class="flex-4">SHREK 2 > ALL THE OTHER SHRECK'S</div>
          </div>
        </div>

        <div v-show="currentSlide === index" class="slide-info" v-else-if="index === 4">
          <img :src="require(`./assets/challenge.png`)" alt="">
        </div>
      </Slide>
    </Carousel>
    <div v-if="currentSlide === 1" class="answer1">
      <p>"[♪ All-Star By Smash Mouth Playing]"</p>
    </div>
    <div v-else-if="currentSlide === 2" class="answer2">
      <p>Selected Date: {{ selectedDate ? selectedDate :  '___________'}}</p>
    </div>
  </div>
</template>

<script>
import { ref , provide} from "vue";
import Carousel from './components/Carousel.vue';
import Slide from './components/Slide.vue';

export default {
  name: 'App',
  components: { Carousel, Slide },
  setup(){
    const selectedDate = ref('');
    const currentSlide = ref(1);

    provide("currentSlide", currentSlide);

    return { selectedDate , currentSlide};
  }
};

</script>

<style lang="scss" scoped>
.carousel {
  display: flex;
  position: relative;
  width: 1000px;
  height: 500px;
  justify-content: center;
  top: 100px;
  margin: 0 auto;
  border-radius: 50px; /* Rounded corners */
  background-color: #F9F9F9;

  .slide-info {
    display: flex;
    position: absolute;
    top: 0; 
    left: 0; 
    width: 100%; 
    height: 100%; 
    justify-content: center;
    align-items: center;
    text-align: center; /* Center text horizontally */

    img {
      max-width: 100%; 
      max-height: 100%; 
      object-fit: cover; /* Cover the entire area of the image container */
    }

    .date-input {
    /* Estilos gerais */
      z-index: 10;
      width: 20%;
      padding: 0.5rem;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 5px;
      background-color: #fff; 
      color: #333; 
    }

    .date-input:hover,
    .date-input:focus {
      border-color: #007bff; 
      outline: none; 
    }

    .date-input:disabled {
      background-color: #eee;
      color: #999; 
    }

    .flexbox-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center; /* Center text horizontally */
    } 

    .flex-1 {
      font-family: "Montserrat", sans-serif;
      font-size: 50px;
      font-weight: bold;
      border-radius: 5px;
      margin-bottom: 20px;
      justify-content: flex-start;
    }

    .flex-2 {
      font-family: "Montserrat", sans-serif;
      font-size: 35px;
      border-radius: 5px;
      margin-left: 60px;
      align-self: flex-start; /* Align to the start of the flex container */
    }

    .flex-3 {
      font-family: "Montserrat", sans-serif;
      font-size: 20px;
      border-radius: 5px;
      margin-left: 100px;
      margin-bottom: 20px;
      flex-shrink: 7; /* Allow shrinking to fit content */
      align-self: flex-start; /* Align to the start of the flex container */
    }
    .flex-4 {
      font-family: "Montserrat", sans-serif;
      font-size: 24px;
      font-weight: bold;
      border-radius: 5px;
      align-self: center;
    }
    .flex-5 {
      font-family: "Montserrat", sans-serif;
      font-size: 24px;
      border-radius: 5px;
    }
  }

  .slide-info p,
  .slide-info label {
    font-family: 'Montserrat', sans-serif; 
    font-size: 50px; 
    font-weight: bold;
  }
}

  .answer1,
  .answer2 {
    position: absolute;
    top: 75%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 10; /* Ensure the answer appears under the carousel */
  }

  .answer1 p,
  .answer2 p {
    font-family: "Montserrat", sans-serif;
    font-size: 24px;
    font-weight: bold;
  }
</style>
