<template>
    <button
        type="button"
        v-if="isLoading == false"
        @click="doClickEvent()"
        :class="bg"
        class="mt-3 flex w-full justify-center rounded-md border border-transparent py-4 px-4 text-sm font-medium text-white shadow-sm  focus:outline-none focus:ring-0 focus:ring-offset-2"
    >
        {{ text }}
    </button>
    <button
        type="button"
        v-if="isLoading == true"
        :class="bg"
        class="mt-3 flex w-full justify-center rounded-md border border-transparent py-4 px-4 text-sm font-medium text-white shadow-sm  focus:outline-none focus:ring-0 focus:ring-offset-2"
    >
        <div class="loader"></div>
    </button>
</template>

<script setup>
const emit = defineEmits([
    'doClick'
])
const props = defineProps({
    text: {
        required: true,
        type: String
    },
    isLoading: {
        required: true,
        type: Boolean
    },
    bg: {
        required: false,
        type: String,
        default: "bg-orange-500 hover:bg-orange-700 focus:ring-orange-500"
    }
})

const doClickEvent = () => {
    emit('doClick')
}
</script>

<style scoped>
/* HTML: <div class="loader"></div> */
.loader {
  width: 20px;
  padding: 3px;
  aspect-ratio: 1;
  border-radius: 50%;
  background: #ffffff;
  --_m: 
    conic-gradient(#0000 10%,#000),
    linear-gradient(#000 0 0) content-box;
  -webkit-mask: var(--_m);
          mask: var(--_m);
  -webkit-mask-composite: source-out;
          mask-composite: subtract;
  animation: l3 1s infinite linear;
}
@keyframes l3 {to{transform: rotate(1turn)}}
</style>