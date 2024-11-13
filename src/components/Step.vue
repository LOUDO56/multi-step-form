<template>
    <div class="flex items-center gap-4">
        <div :class="`${isActive ? 'bg-light-blue text-marine-blue' : 'bg-transparent text-white border border-white'} px-[0.85rem] py-[0.35rem] rounded-full font-bold`">{{ stepCount }}</div>
        <div class="">
            <p class="font-light text-light-gray text-[13px] uppercase">step {{ stepCount }}</p>
            <p class="text-white font-bold tracking-[0.075rem] uppercase text-[15px]">{{ description }}</p>
        </div>
    </div>
</template>


<script setup>

defineProps({
    isActive: Boolean,
    stepCount: Number,
    description: String
})

</script>