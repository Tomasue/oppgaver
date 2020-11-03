<template>
    <div>
        <ul class="collapsible">
            <li v-for="item in items" :key="item.id" :class="{active:item.id === selected}"
                @click.prevent="toggleClass(item.id)">
                <div class="collapsible__header"><i :class="[item.id === selected ? 'minus' : 'plus' ]"></i>Title {{
                    item.id }}
                </div>
                <div class="collapsible__body" :class="{open:item.id === selected}">
                    <div class="body__content">
                        <article class="content__article">
                            <div class="article__media">
                                <img :src="require('../assets/accord-img-' + item.id + '.jpg')" alt="Photo from Pexels.com">
                            </div>
                            <div class="article__info">
                                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Amet architecto, consectetur
                                    expedita laudantium modi mollitia possimus sapiente tenetur voluptate voluptatibus!</p>
                                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Autem, libero.</p>
                                <h4 v-show="item.id === 3">Lorem ipsum dolor.</h4>
                                <p v-show="item.id === 3">
                                    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cum cupiditate
                                    doloremque
                                    laborum quasi ratione voluptas voluptatibus! Architecto consequatur dolorem, eum ipsa
                                    iure repudiandae saepe soluta! Asperiores aspernatur doloremque facilis nemo,
                                    perspiciatis provident repellendus rerum velit voluptate voluptatibus. Ab asperiores
                                    dolor dolore eos, officia provident tempora veniam. Cumque delectus quam voluptate.</p>
                            </div>
                        </article>
                        <article v-show="item.id === 3" class="content__article">
                            <div class="article__media">
                                <img :src="require('../assets/accord-img-2.jpg')" alt="Photo from Pexels.com">
                            </div>
                            <div  class="article__info">
                                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Amet architecto, consectetur
                                    expedita laudantium modi mollitia possimus sapiente tenetur voluptate voluptatibus!</p>
                                <h4>Lorem ipsum dolor.</h4>
                                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Amet architecto, consectetur
                                    expedita!</p>
                            </div>
                        </article>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    let items = [];
    for (let i = 1; i <= 3; i++) {
        items.push({
            id: i
        })
    }

    export default {
        name: 'accordionV2',
        data() {
            return {
                items,
                selected: undefined
            }
        },
        methods: {
            toggleClass(id) {
                this.selected = this.selected === id ? undefined : id;
            }
        }
    }
</script>

<style scoped>
    .collapsible {
        box-shadow: 0 1px 1px 3px rgba(66, 66, 66, 0.08), 0 1px 3px 0 rgba(66, 66, 66, 0.08);
    }

    ul {
        list-style: none;
    }

    .collapsible__header {
        text-align: center;
        display: flex;
        cursor: pointer;
        -webkit-tap-highlight-color: transparent;
        font-weight: bold;
        line-height: 1.5;
        padding: 1rem;
        border-bottom: 1px solid #ddd;
        width: 100%;
    }

    .collapsible__header:hover {
        background-color: rgba(0, 0, 0, 0.2);
    }

    .collapsible__header i {
        margin-right: 10px;
    }

    .collapsible__body {
        display: none;
        border-bottom: 1px solid rgba(66, 66, 66, 0.08);
        width: 100%;
        background-color: rgba(0, 0, 0, 0.02);
    }

    .body__content {
        display: grid;
        grid-template-columns: auto;
        grid-template-rows: auto;
        width: 100%;
        height: 100%;
        padding: 1rem;
    }

    .content__article {
        display: flex;
        justify-content: space-between;
    }

    .article__media {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 10px 0 10px 20px;
    }

    .article__media img {
        width: 300px;
        height: 100%;
        object-fit: cover;
        filter: brightness(90%);
    }

    .article__info {
        font-size: 20px;
        letter-spacing: 1px;
        line-height: 1.5em;
        height: auto;
        font-weight: 300;
        padding: 10px 50px;
    }


    .article__info h2, h4 {
        padding: 10px 0;
        font-weight: bold;
    }

    .plus {
        background: url("../assets/add-24px.svg");
        height: 24px;
        width: 24px;
    }

    .minus {
        background: url("../assets/remove-24px.svg");
        height: 24px;
        width: 24px;
    }

    .open {
        display: block;
        animation: open .5s ease;
    }

    @keyframes open {
        from { opacity: 0; transform: translateY(-20px) }
        to { opacity: 1; transform: translateY(0) }
    }

    @media screen and (max-width: 1024px) {
        .article__media img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 0;
        }

        .article__media {
            margin: 0;
            float: none;
        }

        .article__info {
            font-size: 15px;
            letter-spacing: 1px;
            line-height: 1.5em;
            padding: 20px 0;
            height: auto;
            font-weight: 300;
            float: none;
        }

       .content__article {
           display: flex;
           flex-direction: row;
           flex-wrap: wrap;
           align-items: center;
           text-align: left;
       }
    }

    @media screen and (max-width: 425px) {

    }

</style>