<template>
    <tableDiceRoll :diceCount="diceCount" />
    <buttonDiceRoll :diceCount="diceCount" @emittedRoll="incrementScore" @emittedReset="resetScores" />
</template>

<script setup>
import buttonDiceRoll from './components/buttonDiceRoll.vue';
import tableDiceRoll from './components/tableDiceRoll.vue';
import {reactive} from 'vue';

const diceCount = reactive({
    numberOne: 0,
    numberTwo: 0,
    numberThree: 0,
    numberFour: 0,
    numberFive: 0,
    numberSix: 0,
});

const resetScores = () => {
    Object.keys(diceCount).forEach(key => {
        diceCount[key] = 0;
    });
};

const incrementScore = number => {
    diceCount[Object.keys(diceCount)[number - 1]]++;
};
</script>
