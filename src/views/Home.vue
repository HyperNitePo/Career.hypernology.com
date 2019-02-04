<template>
    <v-content class="pa-0 ma-0">
        <BackGround img="https://career.hypernology.com/img/3dev.jpg" subtitle="爲網絡及Minecraft而開的組織"
                    title="HyperNitePo."></BackGround>
        <History color=""></History>
        <Reason color="grey lighten-2"></Reason>
        <Statistic color=""></Statistic>
        <Recruit color="grey darken-4 white--text"></Recruit>
    </v-content>
</template>

<script>
    import History from "../components/home/History";
    import BackGround from "../components/BackGround";
    import Reason from "../components/home/Reason";
    import Statistic from "../components/home/Statistic";
    import Recruit from "../components/home/Recruit";

    export default {
        components: {Recruit, Statistic, Reason, BackGround, History},
        chname: "Home",
        data(){
            return{
                //
            }
        },
    }
</script>

<style scoped>

</style>