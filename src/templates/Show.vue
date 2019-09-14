<template>
    <div class="scroll-content">
    <a-carousel autoplay :afterChange="reloadme" :centerMode="true" effect="fade" :autoplaySpeed="6000" easing="easeInElastic">
        <div v-for="i in pics">
            <img :src="api + i.pic_dir" width="100%"/>
        </div>
    </a-carousel>
    </div>
</template>
<script>
    import ScrollPosition from '../lib/scroll-position'

    export default {
        name: "Show",
        data() {
            return {
                pics:[],
                // api: process.env.VUE_APP_API_URL,
                api: "http://localhost:82/",
            }
        },
        beforeCreate () {
            this.$http.get('/Pics/get_all_pics')
                .then((response) => {
                    this.pics = response;
                    console.log(response.status);
                })
        },

        methods: {
            reloadme() {
                this.$http.get('/Pics/get_all_pics')
                    .then((response) => {
                        this.pics = response;
                        console.log(response.status);
                    })
            },
        },
        mounted: ScrollPosition.goTop,
    }
</script>
<style scoped>
    /* For demo */
    .ant-carousel >>> .slick-slide {
        width: 100%;
        background: #364d79;
    }

    .ant-carousel >>> .slick-slide  h3 {
        color: #fff;
    }
</style>