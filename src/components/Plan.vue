<template>

    <button @click="$emit('changePlan', {name: name, price: price})" :class="`w-[9.8rem] ${billing === 'monthly' ? 'h-44' : 'h-48'} border rounded-lg px-5 py-5 flex flex-col justify-between items-start ${isActive ? 'border-purplish-blue bg-alabaster' : 'border-light-gray bg-white'} transition duration-200 hover:border-purplish-blue`">
        <div class="w-[2.7rem] mt-1">
            <img :src="iconLink" :alt="`Icon of ${name}`" class="w-full">
        </div>
        <div class="text-left">
            <p class="font-bold text-marine-blue text-lg">{{ name }}</p>
            <p class="text-cool-gray">{{ montlyOrYearly(price) }}</p>
            <p class="text-marine-blue text-sm" v-if="billing === 'yearly'">2 months free</p>
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