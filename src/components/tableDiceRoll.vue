<template>
    <table>
        <tr>
            <th>Number</th>
            <th>Count</th>
        </tr>
        <tr>
            <td>1</td>
            <td>{{ props.diceCount.numberOne }}</td>
        </tr>
        <tr>
            <td>2</td>
            <td>{{ props.diceCount.numberTwo }}</td>
        </tr>
        <tr>
            <td>3</td>
            <td>{{ props.diceCount.numberThree }}</td>
        </tr>
        <tr>
            <td>4</td>
            <td>{{ props.diceCount.numberFour }}</td>
        </tr>
        <tr>
            <td>5</td>
            <td>{{ props.diceCount.numberFive }}</td>
        </tr>
        <tr>
            <td>6</td>
            <td>{{ props.diceCount.numberSix }}</td>
        </tr>
    </table>
</template>

<script setup>
const props = defineProps({
    diceCount: Object,
});
</script>
