<template>
    <div class="filter-container">
        <SortButton
            v-for="sortOption in sortOptions"
            :key="sortOption.type"
            :icon="sortOption.icon"
            :tooltip="sortOption.tooltip"
            :disabled="!modelValue.length"
            @click="sortCards(sortOption.type)" />
    </div>
</template>

<script setup>
import SortButton from './SortButton.vue';

const props = defineProps({
    modelValue: {
        type: Array,
        default: () => [],
    },
});
const emit = defineEmits(['update:modelValue']);

const sortOptions = [
    {
        icon: 'mdi-sort-ascending',
        tooltip: 'Сортировка по возрастанию рейтинга',
        type: 'asc',
    },
    {
        icon: 'mdi-sort-descending',
        tooltip: 'Сортировка по убыванию рейтинга',
        type: 'desc',
    },
    {
        icon: 'mdi-sort-variant-remove',
        tooltip: 'Без сортировки',
        type: 'none',
    },
];

function sortCards(type) {
    let sortedCards;
    switch (type) {
        case 'asc':
            sortedCards = props.modelValue.sort((a, b) => b.rating.rate - a.rating.rate);
            break;
        case 'desc':
            sortedCards = props.modelValue.sort((a, b) => a.rating.rate - b.rating.rate);
            break;
        case 'none':
        default:
            sortedCards = props.modelValue.sort((a, b) => a.id - b.id);
            break;
    }
    emit('update:modelValue', sortedCards);
}
</script>

<style scoped>
.filter-container {
    width: 100%;
    border-radius: 10px;
    background-color: white;
    padding: 10px;
    margin-bottom: 10px;
    display: flex;
    gap: 30px;
    justify-content: center;
}
</style>
