<template>
  <div class="carousel">
    <slot :currentSlide = "currentSlide"/>  
    <!--NAVIGATION-->
    <div class="navigation">
        <div class="toggle-page left">
            <i @click="prevSlide" class="fas fa-chevron-left"></i>
        </div>
        <div class="toggle-page right">
            <i @click="nextSlide" class="fas fa-chevron-right"></i>
        </div>
    </div>
    <!--PAGINATION-->
    <div class="pagination">
        <span 
            @click="goToSlide(index)"
            v-for="(slide, index) in getSlideCount" 
            :key="index" 
            :class="{active : index + 1 === currentSlide}">

        </span>
    </div>
    
  </div>
</template>

<script>
import { ref , onMounted, inject } from "vue"
export default {
    setup(){
        let autoplayInterval;
        const currentSlide = inject("currentSlide");
        const getSlideCount = ref(null);
        const autoPlayEnabled = ref(true);
        const timeoutDuration = ref(20000);

        //next slide
        const nextSlide = () => {
            if(currentSlide.value === getSlideCount.value){
                currentSlide.value = 1;
                return
            }
            currentSlide.value += 1;
            restartAutoplay();
        }

        //prev slide
        const prevSlide = () => {
            if(currentSlide.value === 1){
                currentSlide.value = getSlideCount.value; //OU FICAR NO PRIMEIRO SLIDE
                return
            }
            currentSlide.value -=1;
            restartAutoplay();
        }

        const goToSlide = (index) => {
            currentSlide.value = index + 1;
            restartAutoplay();
        }

        // autoplay
        const autoPlay = () => {
            autoplayInterval = setInterval(() =>{
                nextSlide()
            }, timeoutDuration.value);
        }
        const restartAutoplay = () => {
            clearInterval(autoplayInterval);
                if (autoPlayEnabled.value) {
                    autoPlay();
            }
        };
        if (autoPlayEnabled.value) {
            autoPlay();
        }
        

        onMounted(() =>{
            getSlideCount.value = document.querySelectorAll(".slide").length; //COMENTARARARAR
            //console.log(getSlideCount.value);
        })

        return { currentSlide , nextSlide, prevSlide , getSlideCount, goToSlide};
    }
}
</script>

<style lang="scss" scoped>
    .navigation {
        padding: 0 16px;
        height: 100%;
        width: 100%;
        position: absolute;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .toggle-page {
            display: flex;
            flex: 1;
        }
        .right{
            justify-content: flex-end;
        }

        i{
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            background-color:#9a8ec5 ;
            color: #ffffff;
        }
    }
    .pagination{
        position: absolute;
        bottom: 24px;
        width: 100%;
        display: flex;
        gap:16px;
        justify-content: center;
        align-items: center;

        span{
            cursor: pointer;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background-color: #0000;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
        }
        .active{
            background-color: #cfcdd4;
        }
    }
</style>