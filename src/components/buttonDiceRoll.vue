<template>
    <button @click="rollDice">Throw the dice</button>
</template>

<script setup>
const emit = defineEmits(['emittedReset', 'emittedRoll']);

const rollDice = () => {
    emit('emittedReset');
    for (let i = 0; i < 8; i++) {
        const numberRolled = Math.floor(Math.random() * 6 + 1);
        emit('emittedRoll', numberRolled);
    }
};
</script>
