<template>

    <button @click="$emit('changeSelectionExtra')" :class="`flex items-center rounded-lg justify-between px-5 py-3 lg:px-7 lg:py-5 border ${isActive ? 'border-purplish-blue bg-alabaster' : 'border-light-gray bg-white'} transition duration-200 hover:border-purplish-blue`">
        <div class="flex gap-5 lg:gap-7 items-center">
                <img src="/images/icon-checkmark.svg" alt="icon checkmark" :class="`w-6 h-6 p-1 rounded-md border ${isActive ? 'bg-purplish-blue border-purplish-blue' : 'bg-white border-light-gray'} transition duration-200`">
            <div class="flex flex-col text-left">
                <span class="font-bold text-lg text-marine-blue">{{ title }}</span>
                <span class="text-cool-gray">{{ subtitle }}</span>
            </div>
        </div>
        <div class="text-purplish-blue">
            +{{ montlyOrYearly(price) }}
        </div>
    </button>

</template>

<script setup>

defineProps({
    title: String,
    subtitle: String,
    billing: String,
    price: Number,
    isActive: Boolean,
    montlyOrYearly: Function
})

</script>