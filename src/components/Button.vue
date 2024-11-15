<template>
    <button @click="$emit('nextStep')" :class="`${customColor ? customColor : 'bg-marine-blue'} ${customStyle} text-sm lg:text-base text-white font-bold px-4 lg:px-6 py-3 rounded-md lg:rounded-lg ${customHover ? customHover : 'hover:bg-marine-blue-hover'} transition duration-200`">
        <slot></slot>
    </button>
</template>

<script setup>

defineProps({
    customColor: String,
    customHover: String,
    customStyle: String
})

</script>