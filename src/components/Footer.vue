<template>
    <v-content>
        <v-footer absolute app dark>
            <v-card flat tile class="flex">
                <v-card-title class="grey darken-3">
                    <strong class="display-1 text-uppercase font-weight-medium">Our Ideals</strong>
                    <v-spacer></v-spacer>
                    <span class="headline pt-5 pb-5">
                        We are engineers, thinkers, innovators, intrepreneurs who love doing things that benefits human being.
                    </span>
                </v-card-title>
                <v-card-actions class="black">
                    <p>&copy; HyperNitePo. 2019 - All right reserved.</p>
                    <v-spacer></v-spacer>
                    <v-btn :href="btn.link" :key="i" flat icon large v-for="(btn,i) in social_footer">
                        <v-icon :color="btn.color">{{btn.icon}}</v-icon>
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-footer>
    </v-content>
</template>

<script>
    export default {
        chname: "Footer",
        data() {
            return {
                social_footer: []
            }
        },
        beforeMount() {
            const foot = import('../../public/json/social');
            fetch('/json/social.json').then(r => r.json()).then(data => this.social_footer = data).catch(() => this.social_footer = foot);
        }
    }
</script>

<style scoped>

</style>