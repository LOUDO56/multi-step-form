<template>

    <button @click="$emit('changePlan', {name: name, price: price})" :class="`w-auto lg:w-[9.8rem] h-auto ${billing === 'monthly' ? 'lg:h-44' : 'lg:h-48'} border items-start rounded-lg p-4 px lg:p-5 flex flex-row gap-4 lg:gap-2 lg:flex-col lg:justify-between ${isActive ? 'border-purplish-blue bg-alabaster' : 'border-light-gray bg-white'} transition duration-200 hover:border-purplish-blue`">
        <div class="w-[2.7rem] mt-1">
            <img :src="iconLink" :alt="`Icon of ${name}`" class="w-full">
        </div>
        <div class="text-left lg:text-right">
            <p class="font-bold text-marine-blue text-lg">{{ name }}</p>
            <p class="text-cool-gray">{{ montlyOrYearly(price) }}</p>
            <p class="text-marine-blue text-sm lg:mt-0 mt-0.5" v-if="billing === 'yearly'">2 months free</p>
        </div>
    </button>

</template>


<script setup>

defineProps({
    iconLink: String,
    name: String,
    billing: String,
    price: Number,
    isActive: Boolean,
    montlyOrYearly: Function
})
</script>