<template>
    <main>
        <div class="page-title">
            <h1>Utvikleroppgaver</h1>
        </div>
        <section class="task__1 container">
            <h1 class="task-title">Accordion V1</h1>
            <accordion heading="Title 1"></accordion>
            <accordion heading="Title 2"></accordion>
            <accordion heading="Title 3"></accordion>
        </section>
        <section class="task__1-alt container">
            <h1 class="task-title">Accordion V2</h1>
            <accordion-v2></accordion-v2>
        </section>
        <section class="task__2 container">
            <h1 class="task-title">Carousel</h1>
            <carousel @next="next" @prev="prev">
                <carousel-slide v-for="(img, index) in imgsrc" :key="img.id" :index="index"
                                :currentSlide="currentSlide" @mousemove="drag" @touchmove="drag" @mouseup="endDrag"
                                @touchend="endDrag" :class="[index === currentSlide ? '' : 'opacity']">
                    <img :src="img.src + '&h=1920&w=1080'" :alt="img.alt" class="carousel__image"
                         @mousedown.prevent="startDrag" @touchstart="startDrag">
                </carousel-slide>
            </carousel>
            <carousel-nav>
                <div v-for="(_, i) in imgsrc" :key="_.id" :class="{current:i === currentSlide}"
                     class="carousel__indicator" @click="changeSlide(i)"></div>
            </carousel-nav>
        </section>
        <pre class="value-info container" hidden>
            cursorStartX: {{ cursorStartX}}
            cursorCurrentX: {{ cursorCurrentX }}
            Difference: {{ cursorCurrentX - cursorStartX }}
            Dragging: {{ dragging }}
            Animating: {{ animating }}
            CurrentSlide: {{ currentSlide + 1 }}
        </pre>
    </main>
</template>

<script>

    import Accordion from "./components/Accordion";
    import Carousel from "./components/carousel/Carousel";
    import AccordionV2 from "./components/AccordionV2";
    import CarouselNav from "./components/carousel/CarouselNav";
    import CarouselSlide from "./components/carousel/CarouselSlide";


    const getMouseX = (e) => {
        // Touch (mobile) etc.
        if (e.touches && e.touches.length) {
            return e.touches[0].pageX;
        }
        // mouse
        if (e.pageX && e.pageY) {
            return e.pageX
        }
        return 0;
    }

    export default {
        name: 'App',
        components: {
            CarouselSlide,
            CarouselNav,
            AccordionV2,
            Carousel,
            Accordion
        },
        data() {
            return {
                dragging: false,
                cursorStartX: 0,
                cursorCurrentX: 0,
                animating: false,
                imgsrc: [
                    {
                        id: 1,
                        src: 'https://images.pexels.com/photos/3617457/pexels-photo-3617457.jpeg?auto=compress&cs=tinysrgb&dpr=2',
                        alt: 'Photo by Benjamin Suter from Pexels.com'
                    },
                    {
                        id: 2,
                        src: 'https://images.pexels.com/photos/3573382/pexels-photo-3573382.jpeg?auto=compress&cs=tinysrgb&dpr=2',
                        alt: 'Photo by Josh Hild from Pexels.com'
                    },
                    {
                        id: 3,
                        src: 'https://images.pexels.com/photos/373912/pexels-photo-373912.jpeg?auto=compress&cs=tinysrgb&dpr=2',
                        alt: 'Photo by Burst from Pexels.com'
                    }
                ],
                currentSlide: 0
            }
        },
        computed: {
            slideLen() {
                return this.imgsrc.length;
            }
        },
        methods: {
            next() {
                if (this.currentSlide >= this.slideLen - 1) {
                    // hvis den er på siste sliden vil den loop tilbake til bilde 1(0)
                    this.currentSlide = 0;
                } else {
                    // hvis ikke den er på siste bilde gå til nesten bilde +1
                    this.currentSlide++;
                }
            },
            prev() {
                if (this.currentSlide <= 0) {
                    this.currentSlide = this.slideLen - 1;
                } else {
                    this.currentSlide--;
                }
            },
            changeSlide(i) {
                this.currentSlide = i;
            },
            startDrag(e) {
                this.dragging = true
                this.cursorStartX = getMouseX(e);
                this.cursorCurrentX = this.cursorStartX;
            },
            drag(e) {
                if (!this.dragging) {
                    return;
                }
                this.cursorCurrentX = getMouseX(e);
                this.animating = true;
                let target = e.target ? e.target : e.srcElement;
                if (this.animating) {
                    target.style.transform = "translateX(" + (this.cursorCurrentX - this.cursorStartX) + "px)";
                }
                if (this.cursorCurrentX - this.cursorStartX >= target.clientWidth * 0.3) {
                    if (this.currentSlide >= this.slideLen - 1) {
                        this.currentSlide = 0;
                    } else {
                        this.currentSlide++;
                    }
                    this.endDrag(e);
                } else if (this.cursorStartX - this.cursorCurrentX >= target.clientWidth * 0.3) {
                    if (this.currentSlide <= 0) {
                        this.currentSlide = this.slideLen - 1;
                    } else {
                        this.currentSlide--;
                    }
                    this.endDrag(e);
                }

            },
            endDrag(e) {
                this.dragging = false;
                this.animating = false;
                e.target.style.transform = "translateX(0)";
            }
        }
    }
</script>

<style>
    * {
        /* Reset av elementer slik at jeg ikke trenger å fjerne margins og padding på forskjellige elementer, man kan da bare legge til hvis man trenger.  */
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        background-color: #f5f5f5;
        color: black;
    }

    #app {
        font-family: 'Open Sans', sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }

    .page-title {
        background-color: #131313;
        color: white;
        padding: 20px;
    }

    h1 {
        text-align: center;
    }

    .container {
        width: 80%;
        margin: 0 auto !important;
    }

    .task-title {
        margin: 50px 0;
        text-align: left;
        padding-left: 0;
    }

    .value-info {
        background-color: gray;
        width: 20%;
        font-size: 15px;
        color: yellow;
        padding: 20px 0 0 0;
    }


    @media screen and (max-width: 1024px) {
        .container {
            width: 90%;
            margin: 0 auto;
        }

        .task-title {
        }
    }

    @media screen and (max-width: 425px) {
        .container {
            width: 100%;
            margin: 0;
        }

        .task-title {
            padding: 20px 0;
            margin: 0;
            text-align: center;
        }
    }

</style>
