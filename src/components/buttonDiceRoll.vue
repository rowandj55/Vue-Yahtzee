<template>
    <button @click="rollDice">Throw the dice</button>
</template>

<script setup>
const emit = defineEmits(['emittedReset', 'emittedRoll']);

const rollDice = () => {
    emit('emittedReset');
    const diceRound = [];
    for (let i = 0; i < 5; i++) {
        const numberRolled = Math.floor(Math.random() * 6 + 1);
        diceRound.push(numberRolled);
    }
    emit('emittedRoll', diceRound);
};
</script>
