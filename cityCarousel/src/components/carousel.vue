<template>
    <h1>City Carousel</h1>
    <div class="wholediv">

        <div class="carousel-container">

            <div class="carousel-arrows left-arrow" @click="prevSlide">
                <span class="custom-arrow">&#9756;</span>
            </div>
            <Carousel class="inner" :itemsToShow="itemsToShow" :wrapAround="true" :transition="500" ref="carousel">
                <Slide v-for="(slide, index) in slides" :key="index">
                    <div class="carousel-arrows right-arrow-b" @click="nextSlide">
                        <img src="/assets/images/arrow.png" alt="Right Arrow B" class="custom-arrow">
                    </div>
                    <div class="carousel__item">
                        <div class="card">
                            <div class="card-body">
                                <h3 class="card-title">{{ slide.cardTitle }}</h3>
                                <p class="card-text">{{ slide.cardText }}</p>
                            </div>
                            <div class="card-img">
                                <img :src="slide.imageUrl" class="carousel-img" alt="Image Placeholder">
                            </div>
                        </div>
                    </div>
                </Slide>
            </Carousel>
            <div class="carousel-arrows right-arrow" @click="nextSlide">
                <span class="custom-arrow">&#9758;</span>
            </div>
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'
import { Carousel, Slide, Pagination } from 'vue3-carousel'
import 'vue3-carousel/dist/carousel.css'

export default defineComponent({
    name: 'CarouselDemo',
    components: {
        Carousel,
        Slide,
        Pagination,
    },
    data() {
        return {
            isSmallScreen: false,
            slides: [

                {
                    cardTitle: 'Tokyo, Japan',
                    cardText: 'Tokyo is a bustling metropolis known for its technological advancements, cultural richness, and vibrant city life. It seamlessly blends traditional Japanese culture with modern innovation.',
                    imageUrl: 'pictures/tokyo.png',
                },
                {
                    cardTitle: 'Paris, France',
                    cardText: "Paris is famous for its art, fashion, iconic landmarks like the Eiffel Tower, and its romantic ambiance. City filled with history, culture, and exquisite cuisine.",
                    imageUrl: 'pictures/paris1.png',
                },

                {
                    cardTitle: 'New York City, USA',
                    cardText: "New York City is a global financial hub known for its diverse culture, iconic skyline, and landmarks like the Statue of Liberty and Times Square. The city that never sleeps.",
                    imageUrl: 'pictures/nyc.jpg',
                },
                {
                    cardTitle: 'Rio de Janeiro, Brazil',
                    cardText: "Rio de Janeiro is renowned for its stunning beaches, vibrant carnival celebrations, and iconic Christ the Redeemer statue, a city with a lively atmosphere and natural beauty.",
                    imageUrl: 'pictures/Rio.jpg',
                },

                {
                    cardTitle: 'Dubai, United Arab Emirates',
                    cardText: 'Dubai is known for its modern architecture, luxury shopping, and extravagant lifestyle. It boasts towering skyscrapers, artificial islands, and a dynamic business environment.',
                    imageUrl: 'pictures/Dubai.jpg',
                },
                {
                    cardTitle: 'London, England',
                    cardText: "London is steeped in history, culture, and iconic landmarks like the Tower Bridge and the British Museum. A city that harmonizes tradition with modernity and diverse communities.",
                    imageUrl: 'pictures/London.jpg',
                },
                {
                    cardTitle: 'Toronto, Canada',
                    cardText: "Toronto is a diverse city known for its multiculturalism, iconic CN Tower, and thriving arts scene. The major Canadian city with a blend of urban sophistication and natural beauty.",
                    imageUrl: 'pictures/Toronto.jpg',
                },
                {
                    cardTitle: 'Mumbai, India',
                    cardText: "Mumbai is India's financial powerhouse, known for Bollywood, diverse cultures, and a blend of historic and modern architecture. A city that never fails to captivate with its energy.",
                    imageUrl: 'pictures/mumbai.jpg',
                },


            ],
        };
    },

    created() {
        if (typeof window !== 'undefined') {
            window.addEventListener('resize', this.updateScreenSize);
            this.updateScreenSize();
        }
    },
    destroyed() {
        if (typeof window !== 'undefined') {
            window.removeEventListener('resize', this.updateScreenSize);
        }
    },
    computed: {
        itemsToShow() {
            return this.isSmallScreen ? 1 : 5;
        },
    },
    methods: {
        prevSlide() {
            this.$refs.carousel.prev();
        },
        nextSlide() {
            this.$refs.carousel.next();
        },
        updateScreenSize() {
            this.isSmallScreen = window.innerWidth <= 468;
        },
    }
});
</script>

<style scoped>
@font-face {
    font-family: 'MontserratLight';
    src: url('/assets/fonts/Montserrat-Light.ttf') format('truetype');
}

.wholediv {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 105vh;
    text-align: center;
    padding: 2rem;
}

h1 {
    color: #87314e;
    margin-bottom: 40px;
    text-align: center;
    font-family: 'Dancing Script', cursive;

}

.carousel-card {
    position: relative;
}

.carousel-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 1400px;
}

.carousel__item {
    z-index: 2;
}

.card {
    border-radius: 50px;
    overflow: hidden;
    width: 280px;
    height: 250px;
    align-items: center;
    display: flex;
    flex-direction: column;
    padding: 50px;
    box-sizing: border-box #26a8e000;
    background-color: #fffff5;


}

.card-body {
    text-align: center;
}

.card-text {
    margin-top: 30px;
    font-size: 16px;
    font-family: 'MontserratLight', sans-serif;
    color: #707070;
    margin-bottom: 0;

}

.carousel-img {
    margin-top: 30px;
    width: 100%;
    max-width: 300px;
    object-fit: cover;
}

.inner {
    overflow: hidden;
    width: 1400px;
    align-items: center;
}

.carousel-arrows {
    font-size: 45px;
    cursor: pointer;
}

.left-arrow {
    justify-content: flex-start;
}

.right-arrow {
    justify-content: flex-end;
}

.custom-arrow {
    line-height: 1;
}

.carousel__track {
    transform-style: preserve-3d;
    overflow: hidden;
    min-width: 100%;
    min-width: 1200px;
}

.carousel__viewport {
    perspective: 1000px;
    padding-top: 10px;
}

.right-arrow-b {
    display: none;
}

.carousel__slide {
    z-index: 3;
    transform-style: preserve-3d;
    transform: rotateY(25deg) scale(0.55, 0.55);
    opacity: 0.2;
}

.carousel__slide--prev {
    transform: rotateY(-25deg) scale(0.75);
    z-index: 4;
    opacity: 0.6;

}

.carousel__slide--next {
    transform: rotateY(25deg) scale(0.75);
    z-index: 4;
    opacity: 0.6;

}

.carousel__slide--active {

    transform: rotateY(0) scale(1);
    z-index: 5;
    filter: none;
    border: 2px solid #272625;
    box-sizing: border-box;
    background-color: #EFFFE9;
}


@media screen and (min-width: 2560px) {
    .carousel-container {
        width: 2800px;
    }

    .inner {
        width: 2600px;
    }

    .card {
        width: 400px;
        height: 30vh;
    }

    .card-text {
        font-size: 35px;
    }

    .carousel-img {
        width: 100%;
        max-width: 500px;
    }

    .carousel__slide {
        z-index: 3;
        transform-style: preserve-3d;
        transform: rotateY(20deg) scale(0.65, 0.65);
        opacity: 0.2;
    }

    .carousel__slide--prev {
        transform: rotateY(-20deg) scale(0.85);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--next {
        transform: rotateY(20deg) scale(0.85);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--active {
        transform: rotateY(0) scale(1);
        z-index: 5;
        filter: none;
        opacity: 0.8;
    }
}

@media (max-width: 2860px) {
    .wholediv {
        height: 60vh;
    }

    .card {
        width: 500px;
        height: 650px;
    }
}

@media (max-width: 2560px) {
    .wholediv {
        height: 60vh;
    }

    .carousel-container {
        width: 2400px;
    }

    .inner {
        width: 2200px;
    }

    .card {
        width: 450px;
        height: 25vh;
        padding: 30px;
    }

    .card-text {
        margin-top: 20px;
        font-size: 35px;
    }

    .carousel-img {
        width: 80%;
        max-width: 450px;
    }

    .carousel__slide {
        z-index: 3;
        transform-style: preserve-3d;
        transform: rotateY(20deg) scale(0.65, 0.65);
        opacity: 0.2;

    }

    .carousel__slide--prev {
        transform: rotateY(-20deg) scale(0.85);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--next {
        transform: rotateY(20deg) scale(0.85);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--active {
        transform: rotateY(0) scale(1);
        z-index: 5;
        filter: none;
        opacity: 0.8;
    }
}

@media (max-width: 2060px) {

    .wholediv {
        height: 60vh;
    }

    .carousel-container {
        width: 1800px;
    }

    .inner {
        width: 1600px;
    }

    .card {
        width: 400px;
        height: 500px;
    }

    .card-text {
        margin-top: 10px;
        font-size: 22px;
    }

    .carousel-img {
        width: 100%;
        max-width: 350px;
    }


    .carousel__slide {
        z-index: 3;
        transform-style: preserve-3d;
        transform: rotateY(20deg) scale(0.55, 0.55);
        opacity: 0.2;
    }

    .carousel__slide--prev {
        transform: rotateY(-20deg) scale(0.75);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--next {
        transform: rotateY(20deg) scale(0.75);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--active {
        transform: rotateY(0) scale(1);
        z-index: 5;
        opacity: 0.8;
    }

}

@media (max-width: 1560px) {
    .wholediv {
        height: 60vh;
    }

    .carousel-container {
        width: 1300px;
    }

    .inner {
        width: 1100px;
    }

    /* .card {
        width: 450px;
        height: 350px;
    } */

    .card-text {
        margin-top: 8px;
        font-size: 18px;
    }

    .carousel-img {
        width: 100%;
        max-width: 280px;
    }

    .carousel__slide {
        z-index: 3;
        transform-style: preserve-3d;
        transform: rotateY(20deg) scale(0.55, 0.55);
        opacity: 0.2;
    }

    .carousel__slide--prev {
        transform: rotateY(-20deg) scale(0.75);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--next {
        transform: rotateY(20deg) scale(0.75);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--active {
        transform: rotateY(0) scale(1);
        z-index: 5;
        opacity: 0.8;
    }
}


@media (max-width: 968px) {
    .wholediv {
        height: 60vh;
    }

    .carousel-container {
        width: 900px;
    }

    .inner {
        width: 700px;
    }

    .card {
        width: 360px;
        height: 520px;
        padding: 20px;
        padding-top: 30px;
        padding-bottom: 40px;
        border-radius: 30px;
    }

    .card-text {
        margin-top: 10px;
        font-size: 16px;
    }

    .carousel-img {
        width: 100%;
        max-width: 250px;
    }

    .carousel__slide {
        z-index: 3;
        transform-style: preserve-3d;
        transform: rotateY(20deg) scale(0.55, 0.55);
        opacity: 0.2;
    }

    .carousel__slide--prev {
        transform: rotateY(-20deg) scale(0.75);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--next {
        transform: rotateY(20deg) scale(0.75);
        z-index: 4;
        opacity: 0.6;
    }

    .carousel__slide--active {
        transform: rotateY(0) scale(1);
        z-index: 5;
        opacity: 0.8;
    }

}

@media (max-width: 768px) {
    .carousel-container {
        width: 700px;
        overflow: hidden;
    }

    .card {
        height: 480px;

    }

    .inner {
        width: 500px;
    }

    .card-text {
        margin-top: 5px;
        font-size: 14px;
    }

    .carousel-img {
        width: 100%;
        max-width: 220px;
    }

    .carousel__slide--active {
        transform: translateX(0);
    }

    .carousel__slide--prev {
        transform: translate(-45%) scale(0.85);
        opacity: 0.8;
    }

    .carousel__slide--next {
        transform: translate(45%) scale(0.85);
        opacity: 0.8;
    }

    .carousel__slide--active,
    .carousel__slide--prev,
    .carousel__slide--next {
        transition: transform 0.2s;
    }
}

@media (max-width: 468px) {
    .carousel-container {
        width: 100% !important;
    }

    .inner {
        width: 100% !important;
    }

    .card {
        width: 95%;
        height: 420px;
        border-radius: 30px;
        padding: 10px;
        margin-left: 3%;
        margin-top: 4%;
        margin-bottom: 3%;
    }

    .card-text {
        margin-top: 5px;
        font-size: 14px;
    }

    .carousel-img {
        width: 100%;
        max-width: 180px;
        padding-bottom: 10px;
    }

    .carousel__slide--active {
        transform: translateX(0);
    }

    .carousel__slide--active,
    .carousel__slide--prev,
    .carousel__slide--next {
        transition: transform 0.1s;
    }

}
</style>


