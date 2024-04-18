<template>
    <v-tooltip location="top" :text="tooltip">
        <template v-slot:activator="{ props }">
            <v-btn
                v-bind="props"
                :icon="icon"
                density="compact"
                variant="tonal"
                color="blue"
                :disabled="disabled"
                @click="$emit('click')" />
        </template>
    </v-tooltip>
</template>

<script setup>
const props = defineProps({
    icon: {
        type: String,
        required: true,
    },
    tooltip: {
        type: String,
        required: true,
    },
    disabled: {
        type: Boolean,
        default: false,
    },
});
</script>
