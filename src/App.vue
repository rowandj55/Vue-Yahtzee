<template>
    <div class="groupContainer" id="mainBoard">
        <div class="groupContainer" id="diceBoard">
            <tableDiceRoll class="container" id="diceTableUI" :diceCount="diceCount" />
            <div class="container" id="diceUI">
                <buttonDiceRoll :diceCount="diceCount" @emittedRoll="incrementScore" @emittedReset="resetScores" />
            </div>
        </div>
        <div class="groupContainer" id="scoreBoard">
            <tableUpperScore class="container" :diceCount="diceCount" />
            <tableLowerScore class="container" :diceCount="diceCount" />
        </div>
    </div>
</template>

<script setup>
import buttonDiceRoll from './components/buttonDiceRoll.vue';
import tableDiceRoll from './components/tableDiceRoll.vue';
import tableUpperScore from './components/tableUpperScore.vue';
import tableLowerScore from './components/tableLowerScore.vue';

import {reactive} from 'vue';

const diceCount = reactive({
    numberOne: 0,
    numberTwo: 0,
    numberThree: 0,
    numberFour: 0,
    numberFive: 0,
});

const resetScores = () => {
    Object.keys(diceCount).forEach(key => {
        diceCount[key] = 0;
    });
};

const incrementScore = number => {
    for (let i = 0; i < 5; i++) {
        diceCount[Object.keys(diceCount)[i]] = number[i];
    }
};
</script>
