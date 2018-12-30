<template>
    <v-container class="grid-list-md align-center" :class="$vuetify.breakpoint.mdAndDown ? '' : 'pl-5 pr-5'">
        <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
        <v-flex xs6 class="pa-2">

            <v-timeline align-top :dense="$vuetify.breakpoint.mdAndDown">
                <v-timeline-item color="primary" fill-dot icon="home" >
                    <v-card  class="black">
                        <v-card-title class="title white--text">2014</v-card-title>
                        <v-card-text class="white">ServerHole 正式更名為 HyperNite, 確立新的組織方向。</v-card-text>
                    </v-card>
                </v-timeline-item>
                <v-timeline-item color="warning" fill-dot icon="games">
                    <v-card class="black">
                        <v-card-title class="title white--text">world</v-card-title>
                        <v-card-text class="white"> test hello world</v-card-text>
                    </v-card>
                </v-timeline-item>
                <v-timeline-item color="success" fill-dot icon="games" v-for="i in ($vuetify.breakpoint.mdAndDown ? test : 10)" :key="i">
                    <v-card class="black">
                        <v-card-title class="title white--text">world</v-card-title>
                        <v-card-text class="white"> test hello world</v-card-text>
                    </v-card>
                </v-timeline-item>
            </v-timeline>
            <div class="hidden-md-and-up">
            <v-btn block class="primary elevation-7" large @click="test+=5">Show More</v-btn>
            <v-btn block v-if="test > 0" class="error mt-2 elevation-7" large @click="test=0">Show Less</v-btn>
            </div>
        </v-flex>
        <v-flex xs6 class="pa-2">
            <v-card v-for="i in 5" :key="i" class="mb-3">
                <v-card-title class="black white--text title">標題</v-card-title>
                <v-card-text>
                    <p>內容</p><p>內容</p><p>內容</p><p>內容</p><p>內容</p>
                    <v-spacer></v-spacer>
                    <br>
                    <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
                        <v-flex v-for="i in 4" :key="i" xs3>
                            <v-card class="primary white--text">
                                <v-card-title class="justify-center">{{"button "+i}}</v-card-title>
                            </v-card>
                        </v-flex>
                    </v-layout>
                </v-card-text>
            </v-card>
        </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
    export default {
        name: "Home",
        data(){
            return{
                test: 5
            }
        },
    }
</script>

<style scoped>

</style>