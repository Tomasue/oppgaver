<template>
    <div class="carousel__nav">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: 'carouselNav',
        props: ['currentSlide']
    }
</script>

<style>
    .carousel__nav {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 20px;
        margin-top: 20px;
    }

    .carousel__indicator {
        width: 10px;
        height: 10px;
        background-color: rgba(0, 0, 0, 0.7);
        border: 1px solid rgba(0, 0, 0, 0.9);
        border-radius: 50%;
        margin-left: 10px;
    }

    .carousel__indicator:hover {
        cursor: pointer;
        background-color: rgba(0, 0, 0, 0.8);
        border: 1px solid crimson;
    }

    .current {
        background-color: crimson !important; /* !important fordi noen ganger ville den tro at man forsatt hover på mobilen og ikke bytte farge*/
    }

    @media screen and (max-width: 425px) {
        .carousel__nav {
            padding: 20px 0 10px 0;
        }
    }
</style>