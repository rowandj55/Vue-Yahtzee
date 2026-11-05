<template>
    <div id="diceTable">
        <li v-for="(diceNumbers, number) in props.diceCount" key="number">{{ number }}: {{ diceNumbers }}</li>
    </div>
</template>

<script setup>
const props = defineProps({
    diceCount: Object,
});
</script>
