<template>
    <Teleport to="body">
        <Transition name="modal-outer">
            <div v-show="modalActive" class="absolute w-full h-screen bg-black
            bg-opacity-60 top-0 flex justify-center px-8 ">

                <Transition name="modal-inner">
                    <div v-if="modalActive" class="bg-white self-start mt-32 max-w-screen-md rounded-lg p-4 sm:mt-20">
                        <slot />
                        <button class="text-white bg-weather-secondary mt-8 py-2 px-6 rounded-md"
                            @click="$emit('close-modal')"> Close
                        </button>
                    </div>
                </Transition>
            </div>
        </Transition>
    </Teleport>
</template>

<script setup>

defineProps({
    modalActive: {
        type: Boolean,
        default: false
    }
})
defineEmits(['close-modal'])
</script>

<style scoped>
/* transition sur le bloc parent  */
.modal-outer-enter-active,
.modal-outer-leave-active {
    transition: opacity 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-outer-enter-from,
.modal-outer-leave-to {
    opacity: 0;
}

/* transition sur le bloc enfant ou interne  */
.modal-inner-enter-active {
    transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02) 0.15s;
}

.modal-inner-leave-active {
    transition: all 0.3s cubic-bezier(0.52, 0.02, 0.19, 1.02);
}

.modal-inner-enter-from {
    opacity: 0;
    transform: scale(0.8);
}

.modal-inner-leave-to {
    transform: scale(0.8);
}
</style>