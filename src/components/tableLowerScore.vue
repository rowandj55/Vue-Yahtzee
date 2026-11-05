<template>
    <table>
        <tr>
            <th>Combo</th>
            <th>Score</th>
        </tr>
        <tr v-for="(scoreName, index) in lowerNumbers" :key="scoreName">
            <td>{{ scoreName }}</td>
            <td>{{ lowerScoreUsed[index] }}</td>
            <td><button @click="isLowerScore(index)">Use</button></td>
        </tr>
    </table>
</template>

<script setup>
import {ref} from 'vue';

const props = defineProps({
    diceCount: Object,
});
const lowerNumbers = [
    'Three of a kind',
    'Four of a kind',
    'Full House',
    'Small Straight',
    'Large Straight',
    'Yahtzee',
    'Chance',
];
const lowerScoreUsed = ref(Array(lowerNumbers.length).fill(0));

function isLowerScore(num) {
    switch (num) {
        //Three of a kind
        case 0:
            if (
                Object.keys(props.diceCount).some(
                    x => Object.keys(props.diceCount).filter(y => y === x).length >= 3,
                ) === true
            ) {
                addLowerScore(num);
            }
            break;

        //Four of a kind
        case 1:
            if (Object.keys(props.diceCount).some(x => props.diceCount.filter(y => y === x).length >= 4)) {
                addLowerScore(num);
            }
            break;

        //Full house
        case 2:
            const fullHouseCount = [...new Set(props.diceCount)].map(x => props.diceCount.filter(y => y === x).length);

            if (fullHouseCount.includes(2) && fullHouseCount.includes(3)) {
                addLowerScore(num);
            }
            break;

        //Small Straight
        case 3:
            const isSmallStraight = false;
            for (let i = 1; i < 4; i++) {
                if (
                    props.diceCount.includes(i) &&
                    props.diceCount.includes(i + 1) &&
                    props.diceCount.includes(i + 2) &&
                    props.diceCount.includes(i + 3)
                ) {
                    isSmallStraight = true;
                }
            }
            if (isSmallStraight) {
                addLowerScore(num);
            }
            break;

        //Large Straight
        case 4:
            const isLargeStraight = false;
            for (let i = 1; i < 4; i++) {
                if (
                    props.diceCount.includes(i) &&
                    props.diceCount.includes(i + 1) &&
                    props.diceCount.includes(i + 2) &&
                    props.diceCount.includes(i + 3) &&
                    props.diceCount.includes(i + 4)
                ) {
                    isLargeStraight = true;
                }
            }
            if (isLargeStraight) {
                addLowerScore(num);
            }
            break;

        //Yahtzee
        case 5:
            if (props.diceCount.some(y => props.diceCount.every(x => x === y))) {
                addLowerScore(num);
            }
            break;

        //Chance
        case 6:
            addLowerScore(num);
            break;
        default:
            break;
    }
}

function addLowerScore(num) {
    let total = 0;

    if (num < 2 || num > 5) {
        for (let i = 0; i < Object.keys(props.diceCount).length; i++) {
            total += props.diceCount[Object.keys(props.diceCount)[i]];
        }
    }
    switch (num) {
        case 2:
            total = 25;
            break;
        case 3:
            total = 30;
            break;
        case 4:
            total = 40;
            break;
        case 5:
            total = 50;
            break;
    }
    lowerScoreUsed.value[num] = total;
}
</script>
