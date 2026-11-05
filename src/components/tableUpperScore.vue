<template>
    <table>
        <tr>
            <th>Combo</th>
            <th>Score</th>
        </tr>
        <!-- <tr v-for="number in 6" :key="number"> -->
        <tr v-for="(numberName, index) in upperNumbers" :key="numberName">
            <td>{{ numberName }}</td>
            <td>{{ upperScoreUsed[index] }}</td>
            <td><button @click="addUpperScore(index)">Use</button></td>
        </tr>
        <tr>
            <td>
                Bonus
                <br />
                <span>total score is 63 or more</span>
            </td>
            <td id="fillBonusUpper"></td>
            <td id="bonusActive"></td>
        </tr>
    </table>
</template>

<script setup>
import {ref} from 'vue';

const props = defineProps({
    diceCount: Object,
});
const upperNumbers = ['Aces', 'Twos', 'Threes', 'Fours', 'Fives', 'Sixes'];
const upperScoreUsed = ref(Array(upperNumbers.length).fill(0));

function addUpperScore(num) {
    const upperScore = ref(Array(6).fill(0));
    // console.log(
    //     `checking dice ${Object.keys(props.diceCount)[num]} linked to ${num + 1}, dicethrow is number ${props.diceCount[Object.keys(props.diceCount)[num]]}`,
    // );
    // console.log(`pressed button number ${num + 1}`);
    for (let i = 0; i < 6; i++) {
        if (props.diceCount[Object.keys(props.diceCount)[i]] == num + 1) {
            upperScore.value[i] = props.diceCount[Object.keys(props.diceCount)[i]];
            //console.log(`detected a number for dice ${i + 1}: ${upperScore.value}`);
        }
    }
    upperScoreUsed.value[num] = upperScore.value.reduce((sum, num) => sum + num);
    //console.log(`total value of ${num + 1} throws is ${upperScoreUsed.value[num]}`);
}
</script>
