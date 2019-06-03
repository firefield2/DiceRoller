<template>
    <v-container>
        <v-layout
                class="white rounded-border pa-3"
                align-center
                wrap
        >
            <v-flex sm4 class="text-xs-left text-sm-right">
                <label class="mx-2">Liczba kości:</label>
            </v-flex>
            <v-flex sm4>
                <v-slider class="mx-3 mt-5" :disabled="duringAction"
                          min="1"
                          max="4"
                          always-dirty
                          v-model="slider"
                          thumb-label="always"
                ></v-slider>
            </v-flex>
            <v-flex sm4 class="text-sm-left text-xs-right">
                <v-btn color="success" class="" @click="rollDice">Rzuć kośćmi</v-btn>
            </v-flex>

            <v-flex xs12>
                <div class="text-xs-center mt-2">Suma oczek: <span :key="1" v-if="showSum">{{sum}}</span><span :key="2"
                                                                                                               v-else>...</span>
                </div>
            </v-flex>

        </v-layout>
        <v-layout class="dice-container">
            <v-flex xs12>
                <div class="dice">
                    <die v-for="die in slider" :key="die" :die-number="die" :roll="beginRoll"
                         :selected-dots-count="diceValues"></die>
                </div>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
    import Die from "./Die";

    export default {
        name: "DiceRoller",
        components: {Die},
        data() {
            return {
                slider: 1,
                diceValues: [],
                beginRoll: false,
                duringAction: false,
                showSum: false,
                sum: 0
            };
        },
        watch: {
            slider() {
                this.showSum = false;
            }
        },
        methods: {
            rollDice() {
                this.duringAction = true;
                this.showSum = false;
                let sum = 0;
                for (let i = 0; i < this.slider; i++) {
                    this.diceValues[i] = this.getRandomDiceValue();
                    sum += this.diceValues[i];
                }
                this.sum = sum;
                this.beginRoll = true;
                setTimeout(() => {
                    this.beginRoll = false;
                    this.showSum = true;
                    this.duringAction = false;
                }, 1500);
            },
            getRandomDiceValue() {
                let tempArray = new Uint32Array(1);
                window.crypto.getRandomValues(tempArray);
                let randomValue = tempArray[0] / (0xffffffff + 1);
                return Math.floor(randomValue * 6) + 1;
            }
        }
    };
</script>

<style scoped>
</style>
