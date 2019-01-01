<template>
    <v-container class="grid-list-md align-center" :class="$vuetify.breakpoint.mdAndDown ? '' : 'pl-5 pr-5'">
        <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
            <v-flex class="pa-2" xs5>
                <v-timeline :dense="$vuetify.breakpoint.mdAndDown">
                    <v-timeline-item :fill-dot="history[index].fill_dot" :key="his" :large="!history[index].small_dot"
                                     color="primary" icon="home"
                                     v-for="(his,index) in ($vuetify.breakpoint.mdAndDown ? test : history.length)">
                        <h1 slot="opposite">{{history[index].year}}</h1>
                        <v-card>
                            <v-card-title class="title black white--text">{{history[index].title}}</v-card-title>
                            <v-card-text v-html="history[index].content"></v-card-text>
                    </v-card>
                </v-timeline-item>
            </v-timeline>
            <div class="hidden-md-and-up">
                <v-btn @click="test+=5" block class="primary elevation-7 v-btn--round" large
                       v-if="test < history.length">顯示更多
                </v-btn>
                <v-btn @click="test=5" block class="error mt-2 elevation-7 v-btn--round" large v-if="test > 5">顯示較少
                </v-btn>
                <br>
                <v-divider></v-divider>
            </div>
        </v-flex>
            <v-flex class="pa-2" xs9>
                <v-card :key="i" class="mb-3" v-for="(h,i) in home">
                    <v-card-title class="black white--text title">{{h.title}}</v-card-title>
                <v-card-text>
                    <v-layout :class="($vuetify.breakpoint.mdAndDown ? 'column' : 'row')+' pb-3'"
                              v-if="h.flex.length !== 0">
                        <v-flex :class="box.size" :key="ind" v-for="(box,ind) in h.flex">
                            <v-card :flat="box.flat" :key="ind" class="mb-2" v-for="(card,ind) in box.box">
                                <v-card-title :class="'title '+(card.title_color)+' '+(card.title_text_color)+'--text'">
                                    {{card.title}}
                                </v-card-title>
                                <v-card-text :class="(card.content_color)" v-html="card.content"></v-card-text>
                            </v-card>
                        </v-flex>
                    </v-layout>
                    <span v-html="h.content"></span>
                    <template v-for="(btn,ind) in h.buttons">
                        <v-btn :class="btn.color" :href="btn.link" :key="ind" :to="(btn.router ? btn.link : '' )">
                            <v-icon left>{{btn.icon}}</v-icon>
                            {{btn.chname}}
                        </v-btn>
                    </template>
                </v-card-text>
            </v-card>
        </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
    import history from '../../public/json/history'
    import content from '../../public/json/home'

    export default {
        chname: "Home",
        data(){
            return{
                test: 5,
                history: history,
                home: content
            }
        },
    }
</script>

<style scoped>

</style>