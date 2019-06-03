<template>
    <v-app class="grey">
        <v-content>
            <DiceRoller></DiceRoller>
        </v-content>
    </v-app>
</template>

<script>
    import DiceRoller from "./components/DiceRoller";

    export default {
        name: 'App',
        components: {
            DiceRoller
        }
    };
</script>

<style lang="scss">
    @import "styles/main";
</style>
