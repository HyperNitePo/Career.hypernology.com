<template>
    <v-content>
        <v-parallax :src="img" dark max-height="200">
            <v-layout class="column align-center justify-center">
                <h1 class="font-weight-light display-4 mb-5">{{title}}</h1>
                <h2 class="display-1">{{subtitle}}</h2>
            </v-layout>
        </v-parallax>
    </v-content>
</template>

<script>
    export default {
        name: "BackGround",
        props: {
            img: {
                type: String,
                required: true
            },
            title: {
                type: String,
                required: true
            },
            subtitle: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>