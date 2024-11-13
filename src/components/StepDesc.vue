<template>
    <div class="flex flex-col gap-2">
        <h1 class="font-bold text-marine-blue text-4xl">
        {{ title }}
        </h1>
        <h2 class="text-cool-gray text-lg">
            {{ subtitle }}
        </h2>
    </div>
</template>


<script setup>

defineProps({
    title: String,
    subtitle: String
})

</script>