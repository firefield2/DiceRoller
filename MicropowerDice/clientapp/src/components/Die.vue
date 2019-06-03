<template>
    <ol class="die-list" :class="dieNumber%2>0?'odd-roll':'even-roll'" :data-roll="selectedDieValue" :id="`die-${_uid}`" ref="myRefInside">
        <li class="die-item" data-side="1">
            <span class="dot"></span>
        </li>
        <li class="die-item" data-side="2">
            <span class="dot"></span>
            <span class="dot"></span>
        </li>
        <li class="die-item" data-side="3">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
        </li>
        <li class="die-item" data-side="4">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
        </li>
        <li class="die-item" data-side="5">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
        </li>
        <li class="die-item" data-side="6">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
        </li>
    </ol>
</template>

<script>
    export default {
        name: "Die",
        props: {
            roll: {
                type: Boolean,
                default() {
                    return false;
                }
            },
            selectedDotsCount: {
                type: Array,
                default() {
                    return [(Math.floor(Math.random() * 6) + 1)];
                }
            },
            dieNumber:{
                type:Number,
                default(){
                    return 0;
                }
            }
        },
        computed:{
            selectedDieValue(){
                if(this.roll){
                    this.rollDie();
                }
              return this.selectedDotsCount[this.dieNumber-1]?this.selectedDotsCount[this.dieNumber-1]:(Math.floor(Math.random() * 6) + 1);
            }
        },
        methods: {
            rollDie(){
                this.$refs.myRefInside.classList.toggle("odd-roll");
                this.$refs.myRefInside.classList.toggle("even-roll");
            }
        }
    };
</script>

<style lang="scss">
</style>
