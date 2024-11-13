<template>
    <div class="flex flex-col gap-2">
        <div class="flex justify-between">
            <label :for="name" class="text-marine-blue">{{ name }}</label>
            <p class="font-bold text-strawberry-red">{{ error }}</p>
        </div>
        <input :type="type" :placeholder="placeholder" :name="name" :id="name" @input="handleInput($event)" :value="modelValue" :class="`px-5 py-3 border font-bold ${error === '' ? 'border-light-gray' : 'border-strawberry-red'} rounded-lg text-marine-blue placeholder:text-cool-gray text-lg ring-0 outline-none ${error === '' ? 'focus:border-marine-blue' : ''} transition duration-200`">
    </div>
</template>

<script setup>

defineProps({
    name: String,
    type: String,
    placeholder: String,
    modelValue: String,
    error: String
})

const emit = defineEmits(['update:modelValue']);

const handleInput = ($event) => {
  emit('update:modelValue', $event.target.value)
}

</script>