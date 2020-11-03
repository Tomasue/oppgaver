<template>
    <li v-show="currentSlide === index" class="carousel__slide">
        <slot></slot>
        <p>Slide {{ currentSlide + 1 }} Lorem ipsum dolor sit amet.</p>
    </li>
</template>

<script>
    export default {
        name: 'CarouselSlide',
        props: ['currentSlide', 'index'],
        data() {
            return {}
        }
    }
</script>

<style scoped>

    .carousel__image {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }


    .carousel__slide {
        transition: all 0.4s ease;
        animation: opacity 0.4s ease;
        width: 100%;
        height: 100%;
    }


    @keyframes opacity {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    @media screen and (max-width: 425px){
        p {
            text-align: center;
        }
    }
</style>