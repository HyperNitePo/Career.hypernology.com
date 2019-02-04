<template>
    <v-content :class="color">
        <v-layout class="pl-5 pr-5 pb-5 pt-0" column>
            <v-flex>
                <h1 class="display-2 text-xs-center">本組織內的工作範疇</h1>
                <v-divider dark style="margin: 10px 40%"></v-divider>
                <v-container grid-list-md pa-3>
                    <v-layout :class="isMobile ? 'column' : 'row wrap'">
                        <v-flex :key="i" v-for="(job,i) in jobs" xs4>
                            <v-hover :close-delay="100" :open-delay="70">
                                <v-card :class="'pa-3  '+(hover ? 'white black--text' : 'grey darken-2 white--text')"
                                        hover slot-scope="{hover}" style="min-height: 100px">
                                    <v-layout row>
                                        <v-flex xs2>
                                            <v-btn :dark="!hover" class="transparent" fab flat small>
                                                <v-icon medium>home</v-icon>
                                            </v-btn>
                                        </v-flex>
                                        <v-flex xs10>
                                            <h3 class="headline font-weight-medium">{{job.title}}</h3>
                                            <span :class="'body-2 grey--text '+(hover ? 'text--darken-2' : 'text--lighten-2')">{{job.describe}}</span>
                                        </v-flex>
                                    </v-layout>
                                </v-card>
                            </v-hover>
                        </v-flex>
                    </v-layout>
                </v-container>
            </v-flex>
        </v-layout>
    </v-content>
</template>

<script>
    export default {
        name: "Recruit",
        props: {
            color: {
                type: String,
                required: true
            }
        },
        computed: {
            isMobile() {
                return this.$store.state.isMobile
            }
        },
        data() {
            return {
                jobs: [
                    {
                        title: '行政範疇',
                        describe: '負責管理本組織內部行政架構及進行事務分配，人力資源分配及人力資源管理。',
                        icon: 'home'
                    },
                    {
                        title: '業務範疇',
                        describe: '負責營運本組織的任何大眾經營事務，包括各類伺服器及各大網站經營等。',
                        icon: 'home'
                    },
                    {
                        title: '商務範疇',
                        describe: '與業務範疇不同的是，商務範疇負責營運本組織的公共營利事務，并統計盈利。',
                        icon: 'home'
                    },
                    {
                        title: '技術範疇',
                        describe: '負責提供網絡及電腦技術以支援本組織內的有關業務，或進行編程及軟件開發等事務。',
                        icon: 'home'
                    },
                    {
                        title: '設計範疇',
                        describe: '負責設計網站、影片、圖片及圖示等形象項目，以促進本組織的宣傳事務。',
                        icon: 'home'
                    },
                    {
                        title: '宣傳範疇',
                        describe: '負責為有關本組織內的任何業務進行宣傳工作，例如在各大社交媒體張貼宣傳等等。',
                        icon: 'home'
                    },
                ]
            }
        }
    }
</script>

<style scoped>

</style>