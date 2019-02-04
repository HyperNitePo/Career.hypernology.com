<template>
    <v-content :class="color">
        <v-layout class="pl-5 pr-5 pb-5 pt-0" column>
            <v-flex>
                <v-progress-linear color="black" height="3" indeterminate
                                   v-if="history.length === 0"></v-progress-linear>
                <template v-else>
                    <h3 class="display-2 text-xs-center mb-3">我們的歷史</h3>
                    <v-divider style="margin: 10px 40%"></v-divider>
                    <v-timeline :dense="$vuetify.breakpoint.mdAndDown" class="pl-5 pr-5 ml-5 mr-5">
                        <v-timeline-item :fill-dot="his.fill_dot" :key="i" :large="!his.small_dot"
                                         color="primary" icon="home"
                                         v-for="(his,i) in histories">
                            <h1 slot="opposite">{{his.year}}</h1>
                            <v-card>
                                <v-card-title class="title black white--text">{{his.title}}</v-card-title>
                                <v-card-text v-html="his.content"></v-card-text>
                            </v-card>
                        </v-timeline-item>
                    </v-timeline>
                    <v-btn @click="count+=5" block class="primary elevation-7 v-btn--round" large
                           v-if="count < history.length">顯示更多
                    </v-btn>
                    <v-btn @click="count=5" block class="error mt-2 elevation-7 v-btn--round" large v-if="count > 5">
                        顯示較少
                    </v-btn>
                </template>
            </v-flex>
        </v-layout>
    </v-content>

</template>

<script>
    export default {
        name: "History",
        props: {
            color: {
                type: String,
                required: true
            }
        },
        data() {
            return {
                count: 5,
                history: [],
            }
        },
        computed: {
            histories() {
                return Array.from(this.history).slice(0, this.count);
            }
        },
        beforeMount() {
            fetch("/json/history.json").then(r => r.json()).then(data => this.history = data)
        }
    }
</script>

<style scoped>

</style>