<template>
  <div>
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" stroke-width="1.5" :fill="isFill ? '#333' : 'none'"
      class="w-[18px] h-[18px] dark:!stroke-white stroke-dark-800" >
      <path stroke-linecap="round" stroke-linejoin="round"
        d="M17.593 3.322c1.1.128 1.907 1.077 1.907 2.185V21L12 17.25 4.5 21V5.507c0-1.108.806-2.057 1.907-2.185a48.507 48.507 0 0111.186 0z">
      </path>
    </svg>
  </div>
</template>

<script setup>

const props = defineProps({
  isFill: {
    required: true,
    type: Boolean,
    default: false
  }
})


</script>
