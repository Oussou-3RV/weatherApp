<template>
    <div v-show="modalActive" class="absolute w-full h-screen bg-black
     bg-opacity-30 top-0 left-0 flex justify-center px-8 ">

        <div v-if="modalActive" class="bg-white self-start mt-32 max-w-screen-md rounded-lg p-4">

            <slot/>

            <button class="text-white bg-weather-secondary mt-8 py-2 px-6"
               @click="$emit('close-modal')" > Close
            </button>

        </div>
    </div>
</template>

<script setup>
defineProps({
    modalActive:{
        type:Boolean,
        default:false
    }
})
defineEmits(['close-modal'])
</script>