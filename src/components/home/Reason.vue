<template>
    <v-content :class="color">
        <v-layout class="pl-5 pr-5 pb-5 pt-0" column>
            <v-flex text-xs-center>
                <h1 class="display-2">為何選擇我們</h1>
                <v-divider style="margin: 10px 40%;"></v-divider>
                <span class="subheading">這個世界已經崩壞，萬物枯萎，跌序崩壞，人道毀滅，慘不忍睹，快加入我們，重建世界吧！</span>
                <v-container class="text-xs-left" grid-list-lg>
                    <v-layout :class="isMobile ? 'column' : 'row wrap'">
                        <v-flex :key="i" v-for="(rea,i) in reasons" xs4>
                            <v-expansion-panel dark>
                                <v-expansion-panel-content class="grey darken-3 white--text">
                                    <span class="headline font-weight-light" slot="header">
                                        <v-btn dark fab flat small>
                                                <v-icon medium>{{rea.icon}}</v-icon>
                                            </v-btn>
                                            {{rea.title}}
                                    </span>
                                    <v-divider></v-divider>
                                    <v-card class="white black--text">
                                        <v-card-text>
                                            {{rea.subhead}}
                                        </v-card-text>
                                    </v-card>
                                </v-expansion-panel-content>
                            </v-expansion-panel>
                        </v-flex>
                    </v-layout>
                </v-container>
            </v-flex>
        </v-layout>
    </v-content>

</template>

<script>
    export default {
        name: "Reason",
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
                reasons: [
                    {
                        title: '完善管理',
                        subhead: '我們擁有完善的管理架構以及各式各樣的運作部門。',
                        icon: 'home'
                    },
                    {
                        title: '跨區人才',
                        subhead: '我們組織的人才來自不同地區。',
                        icon: 'home'
                    },
                    {
                        title: '優化設備',
                        subhead: '我們擁有設備齊全的伺服器系統以及完善的管理系統。',
                        icon: 'home'
                    }
                ]
            }
        }
    }
</script>

<style scoped>

</style>