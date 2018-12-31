<template>
    <v-container pl-5 pr-5>
        <v-card>
            <v-stepper v-model="step">
                <v-stepper-header>
                    <v-stepper-step :complete="step > 1" step="1">選擇類別</v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="step > 2" step="2">員工類別</v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step step="3">填寫個人資料</v-stepper-step>
                </v-stepper-header>
                <v-stepper-items>
                    <v-stepper-content step="1">
                        <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
                            <v-flex xs3>
                                <v-btn :class="(departsel.includes(departs[y].id) ? selected : unselect)" :key="y"
                                       @click="" v-for="(x,y) in 4">
                                    {{departs[y].name}}
                                </v-btn>
                            </v-flex>
                        </v-layout>
                    </v-stepper-content>
                    <v-stepper-content step="2">
                        <v-card class="grey lighten-5">
                            <v-card-title>1</v-card-title>
                        </v-card>
                    </v-stepper-content>
                    <v-stepper-content step="3">
                        <v-card class="grey lighten-5">
                            <v-card-title>1</v-card-title>
                        </v-card>
                    </v-stepper-content>
                    <v-btn @click="step++" class="primary" v-if="step < 3">Next</v-btn>
                    <v-btn @click="step--" class="warning" v-if="step > 1">Previous</v-btn>
                </v-stepper-items>

            </v-stepper>
        </v-card>
    </v-container>
</template>

<script>
    import departs from '../../public/json/departments'
    export default {
        name: "Apply",
        data() {
            return {
                departsel: [],
                departs: departs,
                step: 0,
                unselect: ['grey', 'darken-2'],
                selected: ['black']
            }
        },
        methods: {
            click(id) {
                if (!this.departsel.includes(id)) this.departsel.join(id);
                else this.departsel.unshift(id)
            }
        }
    }
</script>

<style scoped>

</style>