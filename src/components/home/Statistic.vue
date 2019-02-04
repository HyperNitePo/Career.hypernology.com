<template>
    <v-content :class="color">
        <v-layout class="pl-5 pr-5 pb-5 pt-0" column>
            <v-flex>
                <h1 class="display-2 mb-3 text-xs-center">我們的數據</h1>
                <v-divider style="margin: 10px 40%"></v-divider>
                <v-container grid-list-lg>
                    <v-layout :class="isMobile ? 'column' : 'row wrap'">
                        <v-flex :key="i" v-for="(stat,i) in stats" xs3>
                            <v-hover>
                                <v-card-title class="headline grey darken-3 white--text justify-center fade-transition"
                                              slot-scope="{hover}">
                                    {{hover ? stat.numbers : stat.title}}
                                </v-card-title>
                            </v-hover>
                        </v-flex>
                    </v-layout>
                    <v-layout :class="(isMobile ? 'column' : 'row wrap')+' mt-3'">
                        <v-flex xs7>
                            <v-card>
                                <v-card-title class="headline black white--text">2018年 全年總盈利報表</v-card-title>
                                <v-layout row text-xs-center>
                                    <v-flex class="align-self-center" xs1>
                                        盈利
                                    </v-flex>
                                    <v-flex xs1>
                                        <template v-for="i in 1000">
                                            <span :key="i+'num'" class="mb-3" v-if="i%100===0">${{1000-i}}</span>
                                            <br :key="i" v-if="i%100===0">
                                        </template>
                                    </v-flex>
                                    <v-flex xs10>
                                        <v-card-text>
                                            <v-sparkline :auto-draw-duration="5000"
                                                         :smooth="5"
                                                         :value="values"
                                                         auto-draw
                                                         color="black"
                                                         line-width="1"
                                                         padding="10"
                                                         v-if="values.length > 2"
                                                         width="300"
                                            >
                                            </v-sparkline>
                                        </v-card-text>
                                        月份
                                        <v-card-title class="black white--text body-2 pa-0 justify-center d-flex">
                                            <span :key="i" v-for="(val,i) in labels">{{val}}</span>
                                        </v-card-title>
                                    </v-flex>
                                </v-layout>
                            </v-card>
                            <v-btn @click="gen_random_value()" block class="primary">重新計算</v-btn>
                        </v-flex>
                        <v-flex xs5>
                            <v-card>
                                <v-card-title class="headline grey darken-3 white--text">這是什麼?</v-card-title>
                                <v-card-text>
                                    這是我們的 2018 年 全年統計收入表。<br>
                                    從上述圖標可見，我們擁有宏大的經濟和創造能力，<br>
                                    能使我們在遇上未來的挑戰時更加積極突破，創造新機遇。
                                </v-card-text>
                            </v-card>
                        </v-flex>
                    </v-layout>
                </v-container>
            </v-flex>
        </v-layout>
    </v-content>
</template>

<script>
    export default {
        name: "Statistic",
        props: {
            color: {
                type: String,
                required: true
            }
        },
        data() {
            return {
                values: [],
                labels: ["一月", "二月", "三月", "四月", "五月", "六月", "七月", "八月", "九月", "十月", "十一月", "十二月"],
                stats: [
                    {
                        numbers: 50,
                        title: '已拯救的國家'
                    },
                    {
                        numbers: 600000,
                        title: '已拯救的人'
                    },
                    {
                        numbers: 39,
                        title: '已拯救的組織'
                    },
                    {
                        numbers: 500,
                        title: '已拯救的地區'
                    }
                ],
            }
        },
        computed: {
            isMobile() {
                return this.$store.state.isMobile
            }
        },
        methods: {
            async gen_random_value() {
                this.values = [];
                while (this.values.length < this.labels.length * 2) {
                    const random = Number.parseInt(Math.random() * 100);
                    this.values.push(random);
                }
            },
        },
        mounted() {
            this.gen_random_value();
        }
    }
</script>

<style scoped>

</style>