<template>
    <details class="accordion">
        <summary>{{ heading }}</summary>
        <div class="accordion__content">
            <img :src="require('../assets/accord-img-1.jpg')" alt="Photo by Benjamin Suter from Pexels.com">
            <div class="content__info">
                <h3>Lorem impsum</h3>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Fugiat laudantium molestias necessitatibus
                    pariatur repudiandae? Dicta dolorem exercitationem ipsum magni reiciendis vero! Assumenda cum dicta
                    dignissimos ducimus numquam odit quasi rem repudiandae suscipit unde. Asperiores, cumque impedit!
                    Aperiam molestiae rem reprehenderit!</p>
            </div>
        </div>
    </details>
</template>

<script>
    export default {
        name: 'accordion',
        props: {
            heading: String,
        }
    }
</script>

<style scoped>
    .accordion {
        transition: all 1s ease-in-out;
    }

    .accordion__content {
        display: grid;
        grid-row-gap: 1rem;
        background-color: #dddddd;
        min-height: 250px;
        padding: 20px 20px;
        grid-template-columns: 1fr 1fr;
    }

    .accordion__content img {
        margin: 0 0 10px 0;
        height: 100%;
        width: 100%;
        object-fit: cover;
        padding: 0 20px;
    }

    .content__info {
        padding: 0 20px;
    }

    summary {
        font-weight: bold;
        padding: 1rem;
        font-size: 20px;
        border: 2px solid gray;
        box-shadow: 0 1px 1px 3px rgba(66, 66, 66, 0.08), 0 1px 3px 0 rgba(66, 66, 66, 0.08);
    }



    summary:hover {
        cursor: pointer;
        background-color: rgba(0, 0, 0, 0.1);
        transition: background-color .3s;
    }
    details
    {
        border-left: 1px solid black;
        border-right: 1px solid black;
    }

    details:last-child {
        border-bottom: 1px solid black;
    }

    details[open] summary ~ * {
       animation: sweep .5s ease-in-out;
    }
    @keyframes sweep {
        0%    {opacity: 0; transform: translateY(-10px)}
        100%  {opacity: 1; transform: translateY(0)}
    }

    summary:focus {
        outline: none;
    }

    summary::-webkit-details-marker {
        display: none;
    }

    summary:after {
        background: url("../assets/add-24px.svg");
        float: left;
        height: 24px;
        width: 24px;
        content: " ";
    }

    details[open] summary:after {
        background: url("../assets/remove-24px.svg");
    }


    @media only screen and (max-width: 768px) {
        .accordion__content {
            display: grid;
            grid-template-rows: 0.5fr 1fr;
            grid-template-columns: 1fr;
            min-height: 200px;
        }

        .accordion__content img {
            height: 200px;
            padding: 0;
        }
    }


</style>