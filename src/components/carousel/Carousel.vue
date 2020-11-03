<template>
    <div class="carousel">
        <button @click="prev" class="carousel__button button--left">
            <img src="../../assets/keyboard_arrow_left-24px.svg" alt="left arrow">
        </button>
        <div class="carousel__slider-container">
            <ul class="carousel__slider">
                <slot></slot>
            </ul>
        </div>
        <button @click="next" class="carousel__button button--right">
            <img src="../../assets/keyboard_arrow_right-24px.svg" alt="right arrow">
        </button>
    </div>
</template>

<script>
    export default {
        name: 'carousel',
        props: ['imgsrc', 'currentSlide'],
        methods: {
            next()  {
                this.$emit('next');
            },
            prev() {
                this.$emit('prev');
            }
        }
    }
</script>

<style scoped>
    .carousel {
        position: relative;
        width: 80%;
        height: 600px;
        margin: 0 auto;
    }

    .carousel__button {
        position: absolute;
        top: 50%;
        transform: translateY(-50%); /* top 50% legger toppen til knappen på midten og midten av knappen så det bruker
        jeg transform får og flytte halve knappe opp slik at den da blir midtstillt */
        border: none;
        background-color: rgba(0, 0, 0, 0.3);
        border-radius: 100%;
        padding: 10px;
    }

    .carousel__button img {
        display: flex;
        justify-content: center;
        align-items: center;
        transition:all 1.0s ease-in-out;
    }

    .carousel__button:hover {
        cursor: pointer;
        background-color: crimson;
    }

    .carousel__button:focus {
        outline: none;
    }

    .carousel__slider-container {
        height: 100%;
        position: relative;
        overflow-x: hidden;
    }

    .carousel__slider {
        list-style: none;
        padding: 0;
        margin: 0;
        overflow-x: hidden;
    }
    .carousel__slide {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
    }


    .button--left {
        left: -100px;
    }

    .button--right {
        right: -100px;
    }


    @media screen and (max-width: 1024px) {
        .carousel {
            height: 400px;
        }

        .carousel__button {
            background-color: rgba(0, 0, 0, 0.3);
        }

        .carousel__button:hover {
            background-color: rgba(0, 0, 0, 0.5);
        }

        .carousel__button:focus {
            -webkit-tap-highlight-color: transparent; /* Hinder default blå rammen rundt et object, slik at det ser litt bedere ut. */
        }

        .button--left {
            left: -50px;
        }

        .button--right {
            right: -50px;
        }
    }

    @media screen and (max-width: 425px) {
        .carousel {
            margin: 0;
            height: 300px;
            width: 100%;
        }

        .button--left {
            z-index: 10;
            left: 10px;
        }

        .button--right {
            z-index: 10;
            right: 10px;
        }

        .carousel__button {
            background-color: rgba(255, 255, 255, 0.5);
        }

        .carousel__button:hover {
            background-color: rgba(255, 255, 255, 0.7);
        }

        .carousel__button:focus {
            -webkit-tap-highlight-color: transparent;
        }
    }

    @media (orientation: landscape) and (max-width: 1024px) {
        .carousel {
            height: 500px !important;
        }
    }

    @media (orientation: landscape) {
        .carousel {
            width: 80%;
            height: 250px;
        }
    }

    @media screen and (min-width: 1440px) {
        .carousel {
            height: 700px;
        }
    }

</style>