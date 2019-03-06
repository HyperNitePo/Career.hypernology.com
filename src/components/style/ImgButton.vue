<template>
    <v-hover>
        <v-card :href="isRoute ? '' : link" :to="isRoute ? link : ''" hover slot-scope="{hover}">
            <v-img :src="src" class="align-center" height="100" position="center center" transition="fade-transition">
                <v-slide-x-transition hide-on-leave leave-absolute>
                    <v-icon dark left v-if="hover">{{!arrow ? 'arrow_forward_ios' : arrow}}</v-icon>
                </v-slide-x-transition>
                <v-slide-x-transition hide-on-leave leave-absolute>
                    <v-icon dark left v-if="!hover">{{icon}}</v-icon>
                </v-slide-x-transition>
                <span class="headline white--text">{{title}}</span>
            </v-img>
        </v-card>
    </v-hover>
</template>

<script>
    export default {
        name: "ImgButton",
        props: {
            isRoute: {
                type: Boolean,
                required: true
            },
            link: {
                type: String,
                required: true
            },
            src: {
                type: String,
                required: true
            },
            title: {
                type: String,
                required: true
            },
            icon: {
                type: String,
                required: true
            },
            arrow: {
                type: String,
                required: false
            }
        }
    }
</script>

<style scoped>

</style>