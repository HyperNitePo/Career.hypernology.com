<template>
    <v-content :class="color">
        <v-layout class="pl-5 pr-5 pb-5 pt-0" column>
            <v-flex text-xs-center>
                <h1 class="display-2">資料連結</h1>
                <v-divider style="margin: 10px 40%;"></v-divider>
                <v-container grid-list-lg>
                    <v-layout :class="isMobile ? 'column' : 'row wrap'">
                        <v-flex xs4>
                            <ImgButton :is-route='true' icon="file_copy" link="/test" src="./img/button/news.jpg"
                                       title="招生公告"></ImgButton>
                        </v-flex>
                        <v-flex xs4>
                            <ImgButton :is-route='true' icon="face" link="/test" src="./img/button/news.jpg"
                                       title="開始應徵"></ImgButton>
                        </v-flex>
                        <v-flex xs4>
                            <ImgButton :is-route='true' icon="group" link="/test" src="./img/button/news.jpg"
                                       title="關於我們"></ImgButton>
                        </v-flex>
                    </v-layout>
                </v-container>
            </v-flex>
        </v-layout>
    </v-content>
</template>

<script>
    import ImgButton from "../style/ImgButton";

    export default {
        name: "Links",
        components: {ImgButton},
        props: {
            color: {
                type: String,
                required: true
            }
        },
        computed: {
            isMobile() {
                return this.$store.state.isMobile;
            }
        }
    }
</script>

<style scoped>
</style>