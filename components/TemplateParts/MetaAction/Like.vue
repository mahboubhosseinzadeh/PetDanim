<template>
  <button
    class="relative min-w-[68px] flex items-center rounded-full leading-none group transition-colors px-3 h-8 text-xs text-neutral-700 bg-neutral-50 dark:!text-neutral-200 dark:!bg-dark-700/20 hover:bg-rose-50 dark:hover:!bg-rose-100 hover:text-rose-600 dark:hover:!text-rose-500"
    title="Liked"
    @click="clickForLike()"
    >
    <Like :isRed="isRed" />
    <span class="ml-1 font-fd">{{count}}</span>
  </button>
</template>

<script setup>
import Like from "@/components/icons/Heart.vue";

const emit = defineEmits([
  "click"
])

const props = defineProps({
  count: {
    required: false,
    type: Number,
    default: 0
  },
  isRed: {
    required: false,
    type: Boolean,
    default: false
  }
})

const clickForLike = () => {
  emit("click")
}
</script>
