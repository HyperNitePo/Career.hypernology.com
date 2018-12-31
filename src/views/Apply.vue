<template>
    <v-container pl-5 pr-5>
        <v-card>
            <v-card-title class="black title white--text">請選擇申請分類</v-card-title>
            <v-card-text>
                <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
                    <v-flex></v-flex>
                </v-layout>
            </v-card-text>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: "Apply",
        data() {
            return {
                items: [
                    '1', '2', '3'
                ]
            }
        }
    }
</script>

<style scoped>

</style>