<template>
        <li v-show="currentSlide === index" class="carousel__slide">
            <slot></slot>
        </li>
</template>

<script>
    export default {
        name: 'CarouselSlide',
        props: ['currentSlide', 'index'],
        data() {
            return {

            }
        }
    }
</script>

<style>

    .carousel__image {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }


    .carousel__slide {
        transition: all 0.4s ease;
        animation: opacity 0.4s ease;
    }

    
    @keyframes opacity {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }
</style>