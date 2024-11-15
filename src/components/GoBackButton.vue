<template>
    <button @click="$emit('previousStep')" :class="`${customStyle} font-bold text-cool-gray text-sm lg:text-lg transition duration-200 hover:text-marine-blue`">Go Back</button>
</template>

<script setup>

defineProps({
    customStyle: String
})

</script>